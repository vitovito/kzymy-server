kzymy-server
============

minimalistic pseudonymous mail exchanger

*kzymy* is a simple mail exchanger system, providing basic email pseudonymity and confidentiality.

It is not meant as a replacement for full *nym* systems: its main goal, instead, is to make
it simple for users to sign up to services that require a valid email address, without having to
use either an email account over which they don't have full control (e.g. a cloud email
service) or an email account on a server traceable back to them.

How kzymy works
---------------

A typical *kzymy*  interaction would be:

* user creates a GPG keypair on a clean virtual machine
* user activates a VPN and/or Tor route
* user connects to a *kzymy* web service (e.g. `kzymy.example.com`)
* user uploads her public GPG key and is allocated a username
* *kzymi* server allocates `username.kzymy.example.com` as mail domain for user
* user creates email addresses under her mail domain
* whenever a message is received for the user, the *kzymy* server encrypts it using the
  user's public key and deletes it
* user checks her inbox by firing up the kzymy-client on her laptop
* if any mail is waiting for pickup, it is fetched by the kzymy-client and
  immediately deleted from the kxymy-server
* on the user's VM, mail is passed on to the local MDA for delivery to the user's inbox

kzymy and privacy
-----------------

*kzymy* only allows users to *receive* emails, which satisfies the main use case:
signing up to online services that require a valid email address, without linking
this email address to the user's identity/location.

This is already possible in multiple ways (nym, Tormail, disposable email addresses,
as well as using a webmail service accessed through a VPN and/or Tor connection, if
an user can trust the webmail provider); *kzymy* provides a simple solution, requiring
minimal setup on the user's side. Users do not need to (and actually should definitely
not) set anything up on the server side: the main architectural benefit of *kxymy* is
to remove any recognizable and trackable link between the server and the client.

No confidentiality of any emails sent to the user is guaranteed (if not encrypted
at the origin, they could be read by eavesdroppers in their route to the *kzymy*
server, or they could be read on the *kzymy* servers either by malicious operators
or because of a server compromise.

However, as long as an user downloads messages from her *kzymy* inbox while
connected via a VPN or Tor, no identity or location information can be linked
to the user's inbox and its contents on the *kzymy* server, and full confidentiality
of message content is preserved between the *kzymy* server and the client on the
user's VM.
