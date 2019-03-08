# Facebook DID Method Specification

**NOTE: This is not a serious proposal for a new DID method, but rather a thought experiment about the nature and objectives of DIDs. Personally, I think it is a contradiction to base DIDs on central registries or platforms such as Facebook or DNS (also see the Abstract of the DID Spec).**

## Author

- Markus Sabadello <markus@danubetech.com>

## Preface

The Facebook DID method specification conforms to the requirements specified in the
[DID specification](https://w3c-ccg.github.io/did-spec/), currently published by the W3C Credentials Community Group.
For more information about DIDs and DID method specifications, please see the
[DID Primer](https://github.com/WebOfTrustInfo/rebooting-the-web-of-trust-fall2017/blob/master/topics-and-advance-readings/did-primer.md).

## Abstract

This specification defines a useful new DID method that allows anyone with a Facebook account to
obtain a Decentralized Identifier (DID), without having to learn complicated new concepts such as 
blockchains or decentralized networks. This will enable the Self-Sovereign Identity (SSI) community
to bootstrap a large number of new users with as little effort as possible, therefore leading to
mass adoption of SSI.

## Example

```json
{
  "@context": "https://w3id.org/did/v1",
  "id": "did:facebook:markus.sabadello",
  "publicKey": [{
       "id": "did:facebook:markus.sabadello#owner",
       "type": "Ed25519VerificationKey2018",
       "owner": "did:facebook:markus.sabadello",
       "Ed25519VerificationKey2018": "CLFRfp2wa3ifbsVvdq52WcpEy7aujactsoqQgxkz7ZKR"
  }],
  "authentication": [{
       "type": "Ed25519SignatureAuthentication2018",
       "publicKey": "did:facebook:markus.sabadello#owner"
  }]
}
```

## Target System

The target system of the Facebook DID method is the Facebook social networking platform which connects people all over the world.

## DID Method Name

The namestring that shall identify this DID method is: `facebook`

A DID that uses this method MUST begin with the following prefix: `did:facebook`. Per the DID specification, this string 
MUST be in lowercase. The remainder of the DID, after the prefix, is specified below.

## Method Specific Identifier

The method specific identifier is a Facebook username. 

	facebook-did = "did:facebook:" facebook-username

### Example

```
did:facebook:markus.sabadello
```

## JSON-LD Context Definition

This DID method specification does not require any new JSON-LD term definitions, but
in future versions may incorporate terms from the Facebook Graph API.
    
## CRUD Operation Definitions

### Create (Register)

Creating a DID is done by publishing a DID Document as a public post on one's Facebook wall, e.g.:

![alt_text](did-method-facebook.png "Facebook post")

### Read (Resolve)

The following steps must be executed to resolve the DID document from a Facebook DID:

1. Construct the URL of the Facebook profile corresponding to the DID, e.g. `https://www.facebook.com/markus.sabadello` for `did:facebook:markus.sabadello`.
2. Retrieve the DID Document posted on the wall of that Facebook profile.

(Whether to use screen scraping, or the Facebook API, or other mechanisms for
retrieving and parsing Facebook posts is a decision that is left to the implementer.)

### Update

The update the DID Document, the DID Document posted on the Facebook wall is edited and re-published.  
Please note that the DID will remain the same, but 
the contents of the DID Document could change, e.g., by including a new verification key or adding service endpoints.  

### Deactivate

To deactivate the DID, the post containing the DID Document is removed from the Facebook wall.

## Security Considerations

Facebook could manipulate your DID Document and track clients that resolve your DID.
