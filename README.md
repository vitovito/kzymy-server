kzymi-server
============

minimalistic pseudonymous mail exchanger

*kzymi* is a simple mail exchanger system, providing basic email pseudonymity and confidentiality.

It is not meant as a replacement for full *nym* systems: its main goal, instead, is to make
it simple for users to sign up to services that require a valid email address, without having to
use either an email account over which they don't have full control (e.g. a cloud email
service) or an email account on a server traceable back to them.

How kzymi works
---------------

A typical *kzymi*  interaction would be:

* user creates a GPG keypair on a clean virtual machine
* user activates a VPN and/or Tor route
* user connects to a *kzymi* web service (e.g. `kzymi.example.com`)
* user uploads her public GPG key and is allocated a username
* *kzymi* server allocates `username.kzymi.example.com` as mail domain for user
* user creates email addresses under her mail domain
* whenever a message is received for the user, the *kxymi* server encrypts it using the
  user's public key and deletes it
* user checks her inbox by firing up the kzymi-client on her laptop
* if any mail is waiting for pickup, it is fetched by the kzymi-client and
  immediately deleted from the kxymi-server
* on the user's VM, mail is passed on to the local MDA for delivery to the user's inbox

