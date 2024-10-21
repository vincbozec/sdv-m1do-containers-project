FROM node:18 AS builder
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

FROM node:18-alpine
WORKDIR /app
COPY --from=builder /app ./

ENV NEXT_PUBLIC_API_BASE_URL=http://api:8000

EXPOSE 3000
CMD ["npm", "start"]
