# Troubleshooting Summary – Domain Controller Discovery Issue

## Problem Observed

The Windows 11 client successfully:
- received an IP address via DHCP
- could ping the Domain Controller by IP address
- could partially resolve the server through DNS

However, the client initially failed to discover the Domain Controller using:

cmd
nltest /dsgetdc:local.lab
