Impacket fork to introduce SPNless-to-SPNless U2U S4U2Proxy in getST.py.

Result: even though RFC 4120 theoretically supports this:

https://www.rfc-editor.org/rfc/rfc4120#section-5.4.1, p. 80:
  
_additional-tickets_
     _Additional tickets MAY be optionally included in a request to the
      ticket-granting server.  If the ENC-TKT-IN-SKEY option has been
      specified, then the session key from the additional ticket will be
      used in place of the server's key to encrypt the new ticket.  When
      the ENC-TKT-IN-SKEY option is used for user-to-user
      authentication, this additional ticket MAY be a TGT issued by the
      local realm or an inter-realm TGT issued for the current KDC's
      realm by a remote KDC.  **If more than one option that requires
      additional tickets has been specified, then the additional tickets
      are used in the order specified by the ordering of the options
      bits (see kdc-options, above).**_

The current Windows implementation of Kerberos doesn't support two additional tickets being sent to the KDC withing the same TGS-REQ (the ST derived from S4U2Self that must be used as authentication proof to invoke S4U2Proxy and the target user's TGT in order to use U2U).

The getST.py file is modified according to RFC and technically correct - in case some day Microsoft decides to implement this. 
Keep in mind that the hypothetical final AP-REQ to the user must also be modified in accordance to the RFC - can't be asked at the moment, but might do it in the future just for funzies.
