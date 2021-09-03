# wormcon0x01
WormCon 0x01 CTF Writeups

# RoboXOR

Rick got a robot named "XORius" as a gift by his parents which activates with a key, in user manual it was written - "we suggest you to use your name is X factor for ROBO ^_^" so Rick followed the user manual, his bot was working fine and now started saying "2506110631060d103c5a15582036045b3c075734640015580d10531e0d1c134a2f"

But now Rick has fear of his parents and he wants your help to understand his ROBO

From the clues, it is assumed to be an XOR cipher
And that the key is "Rick"

Using https://www.dcode.fr/xor-cipher

You will get the answer:
wormcon{n3v3r_g0nn4_6iv3_y0u_up!}

# Network At Risk : Part 4

<< no challenge text >>

Flag Format: wormcon{password_bssid} Note: bssid is in lowecase

1. Download the PCAP file
2. Load into Wireshark
3. Per the challenge clues, we know we are looking at WLAN traffic

In Wireshark, open Wireless->WLAN Traffic

BSSID = ==========================================================================================================================================
Wireless LAN Statistics - challenge.cap:
BSSID  Channel  SSID  Percent Packets  Percent Retry  Retry  Beacons  Data Pkts  Probe Reqs  Probe Resp  Auths  Deauths  Other  Protection
------------------------------------------------------------------------------------------------------------------------------------------
82:25:fa:ee:ed:91        1  DeathStar        99.985194       0.044425      3        1         54           1          25      4     6657     11  Unknown   
82:25:fa:ee:ed:91        1  DeathStar         0.014806       0.000000      0        0          0           1           0      0        0      0            
------------------------------------------------------------------------------------------------------------------------------------------

This will give the BSSID = 82:25:fa:ee:ed:91

For the password,
1. convert the PCAP file to a HCCAPX file

You can use https://hashcat.net/cap2hccapx/ or install the hashcat-utils on your system (https://github.com/hashcat/hashcat-utils/)

Then using HASHCAT, can crack the password against the rockyou dictionary

hashcat --force -a 0 -m 22000 1584_1630218790.hc22000 /usr/share/wordlists/rockyou.txt
** 1584_1630218790.hc22000 is the hccapx file

Eventually, you will get the password and SSID:

bf3af61386189ca5d32058888b9d2ea8:8225faeeed91:dcb72e9c1242:DeathStar:P@$$w0rd

And the final answer is:

wormcon{P@$$w0rd_82:25:fa:ee:ed:91}

# Network At Risk : Part 3

<< missing challenge text>>

download the PCAP file and load it into wireshark

1. Take a look at the protocol hierarchy (under statistics)

I noticed quite a bit of RTP (https://wiki.wireshark.org/RTP)

In wireshark, you can view the audio in the traffic by clicking on Audio->RTP

From here you can play the audio files which repeats "Welcome to the world of voip" over and over

The answer is:

ANSWER: wormcon{welcome_to_the_world_of_voip}

# Network At Risk : Part 2

<< missing challenge text >>
download the PCAP file

Check the protocol hierarchy in the statistics
Noticed there is quite a bit of FTP traffic

Looking at the FTP traffic, I found a couple of things
1. the users password in plaintext
2. a zip file, named backfire.zip, was downloaded

I extracted the raw data for the zip file
unzipped it using the plaintext password found

inside was a text file that had the answer

wormcon{Y0u_4r3_St1LL_US1nG_F7P}

# Wormonetics Part - 1

<< missing challenge text >>
download the image file and load into Autopsy

Flag Format:
Example: Name is Bob and email is hacker@gmail.com
Sample Flag : wormcon{bob_hacker@gmail.com}


** Note: this took awhile, but as information was parsed, I was able to solve the problems.  I never got to load the whole image.

When the emails loaded up, I found one email with the following details

-----HEADERS-----

X-Mozilla-Status: 0001
X-Mozilla-Status2: 00800000
X-Mozilla-Keys:                                                                                 
To: hackwithdark@outlook.com
From: Harry Hacker <harrythehacker1337@outlook.com>
Subject: Regarding The opening
Message-ID: <b247f130-4958-e7c4-278c-fa62e1de08a7@outlook.com>
Date: Fri, 6 Aug 2021 23:38:25 +0530
User-Agent: Mozilla/5.0 (Windows NT 6.3; Win64; x64; rv:78.0) Gecko/20100101 Thunderbird/78.12.0
MIME-Version: 1.0
Content-Type: text/plain; charset=utf-8; format=flowed
Content-Transfer-Encoding: 7bit
Content-Language: en-US

---END HEADERS--

Hello Dark,

Hi want to confirm If I was selected or not

Name = Harry
Email = hackwithdark@outlook.com

This gave me the answer

wormcon{harry_hackwithdark@outlook.com}

