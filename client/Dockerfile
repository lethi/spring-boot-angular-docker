# base image
FROM node:10.13.0

## install Chrome 
#RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -
#RUN sh -c 'echo "deb [arch=amd64] http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list'
#RUN apt-get update && apt-get install -yq google-chrome-stable

COPY package.json package-lock.json ./
RUN npm set progress=false && npm config set depth 0 && npm cache clean --force

## Storing node modules on a separate layer will prevent unnecessary npm installs at each build
RUN npm i && mkdir /ng-app && cp -R ./node_modules ./ng-app

# set working directory
WORKDIR /ng-app

# add `/ng-app/node_modules/.bin` to $PATH
ENV PATH /ng-app/node_modules/.bin:$PATH

# install and cache app dependencies
COPY package.json /ng-app/package.json
#RUN npm install
#RUN npm install -g @angular/cli

# add app
COPY  .  /ng-app

# start app
CMD ng serve --host 0.0.0.0

## Build the angular app in production mode and store the artifacts in dist folder
# RUN $(npm bin)/ng build --prod

## lancer les cmd suivant dans la console:
## Build et étiquetez l'image Docker:
#docker build -t my-image-angular-app .
## run conteneur
#docker run -p 4200:4200  --rm  my-image-angular-app
#docker run -it -p 4200:4200  --rm  my-image-angular-app

## pour volume
#docker run -it -v /ng-app/node_modules -p 4200:4200  --rm  my-image-angular-app
