# Security

With this project, we aim to provide the core guarantees of any secure distributed system:

## Authentication

### Developer <-> Signing Server
The Developer authenticates to the Signing Server with his/her token.
The token is a randomly generated string with arbitrary length that is stored in the Signing Server database along with relevant metadata.
The Signing Server authenticates to the Developer by presenting its X.509 certificate during the TLS handshake phase of HTTP over TLS right before uploading the image file.

### Update Server <-> Signing Server
The Update Server authenticates to the Signing Server by presenting its X.509 certificate during the TLS handshake phase of HTTP over TLS right before uploading the package file.
The Signing Server authenticates to the Update Server with its Signing Server token.
The Signing Server token is a randomly generated string with arbitrary length that is stored in both Server instances' configuration files.

### Update Server <-> Device Daemon
Both authenticate to each other by presenting their X.509 certificates during the TLS handshake phase of HTTP over TLS right before the downloading of the package file.

## Integrity

## Confidentiality
