#base image
FROM node:21

#working directory
WORKDIR /app

#copy the dependencies
COPY package*.json ./

#install the dependencies
RUN npm i

#copy the remaining files
COPY . .

#configure envionment variables
COPY .env.sample .env

#expose the port
EXPOSE 5000

#set the entrypoint
ENTRYPOINT ["npm"]

#set the executable command
CMD ["start"]



