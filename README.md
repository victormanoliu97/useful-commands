# useful-commands

# Install Keycloak server on remote server with HTTPS Disabled
- docker pull quay.io/keycloak/keycloak:latest
- sudo docker run -d --name keycloak -p 9090:8080 -e KC_BOOTSTRAP_ADMIN_USERNAME=admin -e KC_BOOTSTRAP_ADMIN_PASSWORD=admin quay.io/keycloak/keycloak:latest start-dev
- docker exec -it keycloak /opt/keycloak/bin/kcadm.sh config credentials \
  --server http://localhost:8080 \
  --realm master \
  --user admin \
  --password admin
- docker exec -it keycloak /opt/keycloak/bin/kcadm.sh update realms/master -s sslRequired=NONE

# Configure and install MongoDB Community server using Docker/Podman
- docker pull mongodb/mongodb-community-server:latest
- docker run --name mongodb -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=admin -e MONGO_INITDB_DATABASE=admin mongodb/mongodb-community-server:latest
- mongosh
- use admin
- db.auth('admin', 'admin')
- use development
- db.createUser({user: 'victor', pwd: 'victor', roles: [{role: "readWrite", db: "development"}] })
