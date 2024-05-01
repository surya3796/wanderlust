# -------------------- Stage-1: Build Stage -------------------------

#base image
FROM node:21 AS frontend-builder

#working directory
WORKDIR /app

#copy the dependencies
COPY package*.json ./

#install the dependencies
RUN npm i

#copy the remaining files
COPY . .

# --------------------- Stage-2: Final Stage -------------------------

#base image
FROM node:21-slim

#working directory
WORKDIR /app

#copy the above stage
COPY --from=frontend-builder /app .

#configure envionment variables
COPY .env.sample .env.local

#expose the port
EXPOSE 5173

#set the entrypoint
ENTRYPOINT ["npm"]

#set the executable command
CMD ["run", "dev", "--", "--host"]
