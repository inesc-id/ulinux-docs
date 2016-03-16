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

### Image source authentication
Source authentication of the downloaded update image is assured by the verification of its signed SHA512 hash present in the signature file that comes with the update package.

## Integrity
In-transit integrity is assured by the system through the usage of HTTP through TLS.
Integrity of the downloaded update image is assured by the verification of its signed SHA512 hash present in the signature file that comes with the update package. 

## Confidentiality
In-transit confidentiality is assured by the system through the usage of HTTP through TLS. Once an image is downloaded to the device's memory, an attacker may be able to dump it and retrieve its contents.
