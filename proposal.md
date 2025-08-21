# Teaching Email Technology Basics

## Background {#background}

### Origin {#origin}

This idea was submitted by Nobuhiro "Ozi" SUEMASA as an idea for a BoF session at JPAAWG 8. This overview builds on a brief chat about this idea, and hopefully will support further discussion.

### Motivation {#motivation}

Question: How can people learn about fundamental email technologies in 2025?

A generation ago, technically-oriented people who were curious about email could setup their own mail server. Learning how SMTP works often provided a foundation for people going on to learn about other core Internet protocols.

But this can be much more difficult in 2025:
- Home internet connections rarely get static IP addresses
- Most ISPs block SMTP services on port 25/tcp
- Servers exposed to the Internet will be attacked, and may be compromised
- Small servers can be overwhelmed by spam, phishing, etc
- Interacting with major mailbox providers may require email authentication

This document will propose some ways to promote organized and self-directed education about email technologies.

## Audiences {#audiences}

There are a few different types of audiences that may be interested in learning about email technologies.

**Students**: Students may take a class that covers email as one of the fundamental, historically significant Internet protocols.

**Professionals**: Practicing engineers or others who need to use or support email professionally.

**Hobbyists**: People who just want to learn something new, or always wondered how email worked.

Students may take a class that includes a series of exercises exploring email. Professionals may have access to organized tutorials at a conference or similar venue. Hobbyists may want to use a self-paced series of exercises that are flexible enough to fit their schedule.

## Scenarios {#scenarios}

Several scenarios may provide ways for different audiences to meet their needs.

### Collection of VMs {#collectionofvms}

Participants may be given accessed to a set of VMs where they can configure and operate email software: MTAs, IMAP/POP servers, spam filters, etc. These VMs may be segregated from the regular Internet - they may all reside on a private network, or they may be behind a "firewall" of some kind. Or, they may simply run SMTP on alternate ports (e.g. 2525/tcp) and initially be limited to exchanging messages with each other.

This may be more suitable for organized group activities, like a high school or college class, or a conference tutorial.

### BYO Server

Participants may have a Virtual Private Server (VPS), or set up a Raspberry Pi or similar small computer, or host one or more VMs on their own "homelab" server.

This may be necessary to allow self-directed learners to use whatever resources they have available to participate.


## Supporting Materials {#supportingmaterials}

It may be helpful to identify the software and other materials available to use in these exercises.

### Email Software {#emailsoftware}

**Postfix** is a very common MTA, with lots of documentation available. It is capable of supporting the latest email-related protocols while being fairly easy to configure and operate.

**Procmail** is a classic and flexible personal delivery-time agent.

**spamd** or **SpamAssassin** can illustrate common spam-filtering techniques.

**OpenDKIM and OpenDMARC milters** can provide broad email authentication coverage.

### Operating System {#operatingsystem}

Debian Linux and OpenBSD provide very different operating environments, with very different support and configuration procedures. Even within the Linux family, a distro that uses SysVinit or OpenRC will have very different procedures compared to one using Systemd.

It *may* be advisable to specify one operating system to be used, but this needs more discussion.


## Possible Lessons {#possiblelessons}

### Hello, World! {#helloworld}

Start with a walkthrough of the minimum SMTP conversation when submitting a message. Highlight the readable, plain-text (though English oriented) nature of SMTP. Introduce manual SMTP submission using telnet(1) or similar.


### Headers and Envelopes {#headersandenvelopes}

An exploration of the Internet message format (RFC5322) versus the elements of the SMTP protocol (RFC5321).


### Minimum MTA Configuration {#minimummtaconfiguration}

How small can a minimalist configuration be that allows two systems to exchange email via SMTP? Assuming the OS is already installed and configured for the network, this could be a walk-through of a minimum working MTA configuration directives and how they show up in the minimum SMTP conversation.


### Sending Messages {#sendingmessages}

Introduce basic DNS requirements for SMTP. Highlight how MX records work.

In a group context, have the participants send messages to each other. For individual learners, have some automated system they can use to generate messages if they are working in a closed environment.


### Relaying and Forwarding {#relayingandforwarding}

Cover the various ways MTAs may be required to forward messages. Minimal coverage of historical forwarding due to slow/unreliable networks - do mention that open relays existed and why they are bad. Include discussion of routing internal to the organziation, DMZs, etc.


### `president@whitehouse.gov` {#presidentatwhitehousegov}

Explain that SMTP was designed for a "safe" academic and research network. The lack of identity and security in SMTP is arguably the root of all problems with the protocol - but also allowed collaboration like mailing lists and delegated se
nding in the workplace.


### Blocking Messages {#blockingmessages}

Outline several ways to block messages based on the sender. Set the stage for content filtering.

1. Sending address (5322.From) blocking in the MTA
2. Envelope sender (5321.MailFrom) blocking in the MTA
3. Domain blocking (vs. address) in the MTA


### Connection Blocking {#connectionblocking}

Blocking messages based on sending IP address or netblock, in the MTA and also via DNSBLs. Spamhaus, SURBL, etc.


### Using Filters {#usingfilters}

Ways that we might filter based on message content.
1. Personal filtering? (e.g. procmail, sieve)
2. System-level filtering, like milters
3. Discuss external filtering services (appliances, hosted, etc)


### Content Filtering and Spam {#contentfilteringandspam}

Introduce spam and content filtering.
1. Subject vs. body
2. Keyword vs. pattern (regex)
3. Features and scoring (Vipul's Razor)
4. Corpus (Ham/Spam) training with SpamAssassin

