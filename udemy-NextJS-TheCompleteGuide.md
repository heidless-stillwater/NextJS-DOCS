[HOMEPAGE: NextJs](https://nextjs.org/)

[Next.js 15 & React - The Complete Guide](https://www.udemy.com/course/nextjs-react-the-complete-guide/learn/lecture/41160926?start=75#overview)
- RESOUCES:
  - [react-complete-guide-course-resources](https://github.com/academind/react-complete-guide-course-resources/tree/main)
  - [NextJS Essentials: ](https://github.com/mschwarzmueller/nextjs-complete-guide-course-resources)
  - [Rest of the Course: ](https://github.com/mschwarzmueller/nextjs-course-code)
```
npx create-next-app@latest
--
# fails on running http://localhost:3000
# Hydration issue
# interacts badly with 'colorzilla'

--
```

# Section 2: React Refresher
```
npm create vite@latest
--
react-crash-course-v1
react 
javascript
--

cd react-crash-course-v1
npm install
npm run dev

```

###########################
# Dockerfile - ./Dockerfile
#
--# Step 1: Build the React app
FROM node:20 as vite-build

WORKDIR /app

# Copy package.json and package-lock.json (or yarn.lock) files
#COPY package*.json yarn.lock ./
COPY package*.json ./


# Install dependencies
RUN yarn

# Copy the rest of your app's source code
COPY . .

# Build your app
RUN yarn build

# Step 2: Serve the app using Nginx
FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/configfile.template

COPY --from=vite-build /app/dist /usr/share/nginx/html

# Expose port 8080 to the Docker host, so we can access it 
# from the outside. This is a placeholder; Cloud Run will provide the PORT environment variable at runtime.
ENV PORT 8080
ENV HOST 0.0.0.0
EXPOSE 8080
CMD sh -c "envsubst '\$PORT' < /etc/nginx/conf.d/configfile.template > /etc/nginx/conf.d/default.conf && nginx -g 'daemon off;'"

--

####################
# NGINX - nginx.conf
#
--
server {
    # listen       ${PORT};
    listen       443;

    server_name  localhost;

    location / {
        root   /usr/share/nginx/html;
        index  index.html index.htm;
        try_files $uri /index.html;
    }
}

--

###########
# BUILD/RUN
#

# local
npm run dev

# docker
npm run build   # generate 'dist/'

docker build -t arjuna11/react-crash-course-v1:latest .
docker run -p 8080:443 arjuna11/react-crash-course-v1:latest

# check local deploy
http://127.0.0.1:8080

# GCP: CloudRun->DeployContainer->CreateService->ContinuouslyDeploy
```
Region: europe-west2
Allow Unauthenticated Invocations
EditContainer->ContainerPort->'443'
CREATE
```







