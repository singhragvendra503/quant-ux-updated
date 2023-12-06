FROM node:16-alpine

# Install required packages and set up environment
RUN apk --no-cache add git bash \
    && rm /bin/sh && ln -s /bin/bash /bin/sh

# Set timezone
ENV TZ=America/Chicago

# Create the application directory
WORKDIR /usr/src/quant-ux

# Set ENV vars here
ENV QUX_PROXY_URL=http://qux-be.quantux.com:8080

# Clone the frontend repo, install dependencies, and build
RUN git clone https://github.com/singhragvendra503/quant-ux.git \
    && cd quant-ux \
    && npm install \
    && npm run build

# Expose the Web Port
EXPOSE 8082

# Start the server running
CMD [ "node", "quant-ux/server/start.js" ]
