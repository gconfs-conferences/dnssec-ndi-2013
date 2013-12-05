% Why DNSSEC is awesome
% Paul "Dettorer" Hervot
% 2013-12-06

# Basic DNS architecture
## The problem: DNS spoofing
### Domain Name System
\begin{figure}[htbp]
\centering
\includegraphics[height=6cm]{imgs/Recursive.png}
\caption{Basic DNS architecture}
\end{figure}

### DNS spoofing (or cache poisoning)
\begin{figure}[htbp]
\centering
\includegraphics[height=6cm]{imgs/cahe_poisoning_orig.png}
\caption{DNS Spoofing: the idea}
\end{figure}

# Solution: DNSSEC
## The idea
### Signature
- A Cryptographic signature for each record set (RRSIG records)
- A public signature to decode RRSIGs (DNSKEY records)

### Chain of trust
- To validate the public key, the validator goes through the chain of trust.
    - It usually begins with the root DNS serveurs.
    - The chain is symbolized with the DS record.

## But wait… there's more !
### DANE
- DNS-Based Authentication of Named Entities
    - Self-signed VALID SSL certificates (TLSA records)
    - SSH fingerprints (SSHFP records)
    - PGP signatures (PKA records)

## A few disadvantages
### The chain of trust
- Each secure lookup needs to go through the whole chain.
\begin{figure}[htbp]
\centering
\includegraphics[height=5cm]{imgs/Recursive.png}
\caption{Basic DNS architecture}
\end{figure}

### DNS amplification
- Signing records generate much more data.

### Zone walking
- The NSEC record
- Better: the NSEC3 record

## Let's check !
### With dig
- dig +topdown +sigchase dettorer.net

### In navigators
- Firefox plugin: DNSSEC validator
- TLSA is not yet implemented in navigators.
    - It's in project for at least Firefox and Google Chrome

### Questions ?
- dettorer@dettorer.net
- \#epita @ irc.rezosup.org
- Slides on http://gconfs.fr
