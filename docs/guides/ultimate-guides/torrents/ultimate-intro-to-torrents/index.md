---
slug: ultimate-intro-to-torrents
title: The Ultimate Intro to Torrents
tags: [torrent, tutorial]
authors: TechSquidTV
---

# What is a Torrent?

You've likely heard of torrents before, perhaps even used them in the past. Torrents provide a method of sharing files, usually larger ones, directly with other "peers" over the internet. They eliminate the need for a costly central server. 
But how do they function? What advantages do torrents offer? How can one utilize them? Are they secure? Consider the following as your comprehensive guide to _torrents_.


## The Background of BitTorrent

In the late 90s [Bram Cohen](https://en.wikipedia.org/wiki/Bram_Cohen) ([twitter](https://twitter.com/bramcohen)), a software developer, was working for a company called [MojoNation](<https://en.wikipedia.org/wiki/Mnet_(peer-to-peer_network)#MojoNation>) that was trying to create an encrypted decentralized file storage system for commercial-use.
Unfortunately, the company was faced with severe financial difficulties and would close in 2002.
Just before then, Cohen would realize that the technology he had been working on, while not a commercial success, could be used to create a new file sharing protocol that could dramatically speed up the process of sharing large files, such as [porn collections](https://www.wired.com/2005/01/bittorrent-2/).
Other peer-to-peer file sharing protocols at the time existed, such as ["Kazaa"](https://en.wikipedia.org/wiki/Kazaa), but they all were dependent on downloading complete files from a single user or "peer".
Especially at the time, with the majority of people having slow and unreliable internet access, the process of downloading large files could, and usually did, take a very long time.

Cohen would leave MojoNation in 2001 and begin work on the open protocol that would become known as [BitTorrent](https://en.wikipedia.org/wiki/BitTorrent).
BitTorrent would immediately become popular with the Linux community, as it allowed for the free distribution of Linux distributions and other free software that would not have had the funding or labor to distribute their software otherwise.
And by 2003, [ThePirateBay](https://en.wikipedia.org/wiki/The_Pirate_Bay) would launch, becoming one of the most infamous websites in the world to download free _pirated_ content, such as music, movies, and TV shows.

## BitTorrent Basics

BitTorrent decentralizes the file sharing process. 
Rather than one server being required to serve a file to many users, which can become bottle necked, BitTorrent allows for many users to share files with each other by joining a "swarm".
Users within the swarm can advertise they have a file, or a part of it, and exchange "pieces" with other users in the swarm.

![BitTorrent Swarm](./img/tracker-light-mode.svg#gh-light-mode-only)![BitTorrent Swarm](./img/tracker-dark-mode.svg#gh-dark-mode-only)

### Torrent files

In order to distribute a file using BitTorrent, a ["torrent"](https://en.wikipedia.org/wiki/Torrent_file) file is created, which contains metadata about the file(s) to be shared.
You can use a tool such as [TorrentEditor](https://torrenteditor.com/) to view the contents of a torrent file online. Here for example is the contents of the Ubuntu 23.04 Server ISO.

:::info

#### Ubuntu 23.04 Live Server Torrent Details

**Filename:** ubuntu-23.04-live-server-amd64.iso.torrent

##### Hash Details

**Info Hash:** D6B4535B A8F2B340 12BC6335 69F113E7 7017E032

##### Tracker Information

**Tracker URL:** https://torrent.ubuntu.com/announce

**Seeds:** 158, **Peers:** 4, **Completed:** 1

Additional Tracker: https://ipv6.torrent.ubuntu.com/announce

**Seeds:** 158, **Peers:** 4 **Completed:** 1

##### Metadata

- **Created On:** 04/20/23 12:14:49
- **Created By:** mktorrent 1.1
- **Comment:** Ubuntu CD releases.ubuntu.com
- **Piece Length\*:** 256 KB
- **Private\*:** Off - Unset

##### Files

**Filename:** ubuntu-23.04-live-server-amd64.iso

**File Size:** 2.46 GB
:::

The torrent file itself is incredibly small, for this 2.46 GB ISO the torrent itself is only 200 KB.

### Magnet links

The data inside a torrent file is so small, that it can, in fact be can be represented as a URL rather than a file. 
A ['Magnet link'](https://en.wikipedia.org/wiki/Magnet_URI_scheme) is a URL scheme that allows you to share information about a torrent as a link, rather than a file.
This means websites that want to share torrents, no longer had to worry about serving files, making it extremely robust to simply share a _static_ webpage with links to all the files you want to share, the most simple form of a website.
Static webpages are extremely easy and cheap to host, robust against traffic spikes and take-down attempts, and can often even be hosted for free on a number of services online. Becoming so lightweight, it became trivial to put up "mirrors", or copies of the website under different domain names, often hosted in different countries, to ensure the website would never go down.
This helped make torrent indexers like ThePirateBay _decentralized_. In 2012, in an effort to ensure the longevity of the content on ThePirateBay and thanks to their recent conversion to magnet links, their website was replicated by users and [reduced to a 90 MB torrent file](https://torrentfreak.com/the-pirate-bay-returns-121213/) that anyone could copy and re-host.

A magnet link works similar to how if you have ever clicked on an email address in the browser before and had it open up your default email client.

If you have never seen an email link before, it looks like this:

```html
<a href="mailto:x@y.com">x@y.com</a>
```

If you click on that link, it will open up your default email client and create a new email to the address.

Similarly, a magnet link looks like this:

```html
<a href="magnet:?xt=urn:btih:222FGW5I6KZUAEV4MM2WT4IT45YBPYBS&dn=ubuntu-23.04-live-server-amd64.iso&xl=2641264640&tr=https%3A%2F%2Ftorrent.ubuntu.com%2Fannounce">ubuntu-23.04-live-server-amd64.iso</a>
```

This link, when clicked, will launch your system default torrent client and begin downloading the file.

If you take a closer look at the magnet link, you'll notice it contains all the same information as the torrent file, but in a URL format.

#### Magnet Link Parameters

##### xt (Exact Topic)

The `xt` parameter is used to identify and verify the file(s) via a [URN](https://en.wikipedia.org/wiki/Uniform_Resource_Name). In all _torrent_ related magnet links, this will be a `urn:btih:` followed by the [SHA-1](https://en.wikipedia.org/wiki/SHA-1) info hash of the torrent. `btih` here stands for "BitTorrent Info Hash", and would differ from different older P2P protocols. This is all you need to download a torrent, but the other parameters are useful for providing additional information about the torrent.

##### dn (Display Name)

The `dn` parameter is used to provide a display name for the torrent. This is the name that will be displayed in your torrent client. If this parameter is not provided, the name of the file will be used instead.

##### xl (eXact Length)

The `xl` parameter is used to provide the size of the file in bytes. This is useful for your torrent client to know how much data to expect to download.

##### tr (Trackers)

The `tr` parameter is used to provide a list of trackers to connect to.

##### More Info

These are the main parameters you will likely see in most magnet links, though more do exist.
For more information on the magnet link parameters, see the [Magnet URI scheme](https://en.wikipedia.org/wiki/Magnet_URI_scheme#Parameters) Wikipedia page.

### Pieces



### Torrent Clients

If you were downloading a typical file from the internet, you would likely use a web browser to grab the file, save it to your computer and then end communication with the server.
BitTorrent is different, as it is a peer-to-peer protocol, you are not just downloading a file from a server, you are also uploading the file to other users.
To do so, you'll need a BitTorrent client, some software that can communicate with other users and share the file.

There are many BitTorrent clients available, but the most popular these days are:
  - [Transmission](https://transmissionbt.com/)
  - [Deluge](https://deluge-torrent.org/)
  - [qBittorrent](https://www.qbittorrent.org/)

### Torrent Tracker

In order to begin downloading a file via torrent, you need to connect with other "peers" or users in the swarm who have "pieces" of the file you want.
A "[tracker](https://en.wikipedia.org/wiki/BitTorrent_tracker)" is a web server that keeps track of members in a swarm and aids in connecting users together based on which pieces of the file they have.

When a torrent client initiates a download from a torrent file, it will first connect to the tracker and announce that it is joining the swarm and what pieces of the file it has available, if any.
The tracker will respond with a list of peers that the client can connect to and begin downloading the file from. Once the client and a peer have connected, they no longer require the tracker to communicate with each other. However, the client will continue to communicate with the tracker to update it on the pieces it has available and to receive a list of new peers to connect with.

If a tracker were to go down before you got the chance to connect to the swarm, it might be very difficult to find other peers to connect with. You'll notice most torrent files will have multiple trackers listed to ensure longevity of the torrent. If all trackers were offline, it would still be possible to join the swarm if your client was aware of at least one other peer in the swarm. Luckily, this is where the [DHT](#dht-distributed-hash-table) comes in.

### DHT (Distributed Hash Table)

A [DHT](https://en.wikipedia.org/wiki/Distributed_hash_table) is a decentralized system for storing and retrieving simple key-value data, where any member of the network can retrieve data from any other member of the network. In BitTorrent, the [Mainline DHT](https://en.wikipedia.org/wiki/Mainline_DHT) protocol is used to store information about torrents and their peers locally. The DHT works as an alternative to a tracker and can aid in connecting to a swarm if the tracker is offline.

To find peers for a particular swarm over DHT, a `get_peers` query is made with the SHA-1 hash of the torrent (the "infohash") as the key to the "nearest" node in the DHT. The node will then respond with a list of peers in the swarm. If the node does not have any peers, it will respond with a list of other nodes in the DHT that are closer to the infohash. The client will then query those nodes for peers and continue until it has found peers to connect with. An algorithmic virtual game of telephone. It is important to note that "nearest" in the context of the DHT is not related to physical geographical distance, but instead a mathematical distance that creates efficient and balanced routing.

![DHT Request](./img/dht-diagram-dark-mode.svg#gh-dark-mode-only)![DHT Request](./img/dht-diagram-light-mode.svg#gh-light-mode-only)

### Leechers and Seeders

BitTorrent is built around the idea of users sharing files with each other. The system only works if users are willing to share the files they have downloaded with other users.

A "leecher" is a name typically given to users who download files and immediately stop sharing them. A "leech" is someone who takes from the BitTorrent network without giving back.

If you are still actively downloading a file and simultaneously uploading to other peers, you are commonly referred to as a "peer". A peer generically refers to any user in a swarm, but is often used to refer to users who are still downloading the file.

Finally, a "seeder" is a user who has completed downloading a file and continues to share the file with other users. Because of the decentralized nature of BitTorrent and the concept of "pieces", it is extremely beneficial to have seeders in the swam who have full copies of the file. Without enough seeders in a swarm, it is common for all active members in a swarm to exchange pieces with each other, but if no user has the complete file, it is possible that no user will ever complete the download.

### Private Trackers

A private tracker refers to a Tracker, usually backed by a website or community, that requires registration to login and access. When downloading torrents from a private torrent tracker website, the tracker URL is usually unique to your account and is used to track your ratio of upload to download. While limiting the amount of users who can join may appear counter-intuitive to the decentralized nature of BitTorrent, private trackers often mitigate a small portion of privacy concerns by ensuring non-community members are not able to spy on the activity in the swarm.

It may go without saying that private trackers are usually closed to registration, requiring an invite from an existing member to join, or some trackers will open registration for a short period of time to allow new members to join.

In private tracker environments, it may be that your tracker requires you to maintain a certain ratio of upload to download. It is usually the case that you must at least upload as much as you download, or otherwise face some penalty, such as being banned from the tracker.

## Torrenting Safely

Torrenting is a great way to download files, but it is important to be aware of the risks involved. While torrenting itself is not illegal, it is often used to download pirated content, which is illegal in many countries. Additionally, because of the decentralized nature of BitTorrent, it is possible for malicious users to join a swarm and spy on the activity of other users. This is especially concerning when downloading pirated content, as it is possible for a malicious user to join the swarm and record the IP addresses of other users in the swarm. This is why it is important to use a VPN when torrenting or some other method of obscuring your IP address.

We will update this guide in the future with links to a VPN specific guide.