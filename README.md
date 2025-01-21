This is a starter template for [Learn Next.js](https://nextjs.org/learn).


FROM node:23-alpine
RUN mkdir -p /home/node/app/node_modules && chown -R node:node /home/node/app
WORKDIR /home/node/app
COPY package*.json ./
#RUN npm install
RUN npm install
RUN npm i next@latest
#RUN npm run build
COPY --chown=node:node . .
EXPOSE 3000
CMD ["npm", "run", "start"]



services:
  node:
    build: .
    command: "npm run dev"
    working_dir: /home/node/app
    environment:
      - NODE_ENV=production
    expose:
      - "3000"
    ports:
      - "3000:3000"


next.config.mjs:
/** @type {import('next').NextConfig} */
const nextConfig = {
  output: "export",
  env: {
    API_UTILS_URL: process.env.API_UTILS_URL    
  }
};
export default nextConfig;
