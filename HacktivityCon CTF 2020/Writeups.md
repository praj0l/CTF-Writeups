# OSINT:
## Whale Watching:
> Where is the flag? It is not down on any map; true places never are.<br>
> Hunt down:<br>
> `johnhammond/whale_watching`

For this challenge I searched for the username 'johnhammond' using `sherlock` (`python sherlock johnhammond`). After going through the results one by one and following the links to the doubtful websites, I came across `docker`, which had `whale_watching` repository. Without searching anywhere on the website I had begun downloading the repository. Since the download size was a bit large, I decided to check different places on the website waiting for the download to finish. Then I found the flag which you can see using the following link, and, yeah, I cancellled the download.

[johnhammond/whale_watching](https://hub.docker.com/layers/johnhammond/whale_watching/latest/images/sha256-2b7db5e2796fbbd0616d5279b81f0ae151f4a52ad3e0325de7f583ce94848ddd?context=explore)

```
flag{call_me_ishmael}
```

<hr>

## World Hotspots:
> What can you tell me about `9C:EF:D5:FB:9F:F0`?

This took me a lot of time to figure out. After searching a lot I had still not been able to find the website where I could search for this BSSID to get the flag. All the websites when searched for it gave me the name of the vendor, but no device details. I even used [wigle](https://wigle.net) but could not find the expected details. Later I asked my teammate and brother and he said that I had to search for it in `wigle` using "Advanced search", the only thing I had missed in that website! Screenshot in wigle: [here](/files/world_hotspots_flag.png)

```
flag{network_osint}
```


<hr>
    
    
# Warmups:
## CaesarMirror:
> Caesar caesar, on the wall, who is the fairest of them all?<br> 
> Given file+Solution: [caesarmirror.txt](/files/caesarmirror.txt)

To solve the challenge I applied Caesar Cipher with shift by 13 aka ROT13 to decipher the given text, which gave half readable English text and half like nonsense text. But after trying to make sense of the nonsense text I came to realize that it was English text in reverse direction or in Arabic style. So I ended up reversing the half part and got the flag. [Here is](/files/caesarmirror) what I got at last.

```
flag{julius_in_a_reflection}
```

<hr>


## InternetCattos:
> The Internet is full of wonderful kittens and cattos. You can even find one at `jh2i.com` on port `50003`!

Initially `nc jh2i.com 50003` did not give anything except the line:
> Oh, we already sent the flag! Did you see it?

It was suspicious, so I channeled the output from `netcat` to a text file:

```
nc jh2i.com 50003 > textfile.txt
```

Opening the text file gave the flag but each character on a line. Thus all the characters when merged to a single line gave the flag in full.
Result: [internetcattos.txt](/files/internetcattos.txt)

```
flag{this_netcat_says_meow}
```

<hr>


## Vencryption:
> I know the flag is in this file! I just cannot open it for some reason...<br> 
> Given file: [vencrypted.txt](files/vencrypted.txt)

I had to search for this encryption because I had never heard of it. So, after a little more search to find a way to decrypt this encryption(vim encryption), I came across a [Python script from nlitseme](https://github.com/nlitsme/vimdecrypt). Then I made a little change on the script(he has updated it now): replaced `time.clock()` with `time.perf_counter()` as the former had been deprecated long Python versions ago. Finally, I started the bruteforce job with this script and a very good word-list that I found after searching for some time. The script was able to find the password after 77000 tries that lasted for more than 10 minutes, I guess. It also decrypted the given text which was the flag.

[Screenshot: After 77000 tries!](/files/flag%20after%2077000%20tries.png)

`password: computer`

```
flag{sometimes_it_really_do_be_like_that_tho}
```

<hr>


## Hexgedit:
> Woah! Someone opened the flag file in hexedit... and then gedit?? <br>
> Given image: [hexgedit.png](/files/hexgedit.png)

After initial examinations for any steganographic clues failed, I proceeded with copying character by character whatever was on the picture/image to my text editor. I used hex to text conversion tool to convert the hex values, which I was able to copy taking hours, and there was the flag.
Result: [hexgedit.txt](/files/hexgedit.txt)

```
flag{optical_hexadecimal_recognition_amirite}
```


Since I had forgotten that I could simply scan the image using an online OCR tool to get the hex text easily, I wasted hours copying each character to my text editor. Point to remember for future.


<hr>


## Private Investigator:
> We have hired you to help investigate this private key. Please use it to connect to the server like so:<br>
> `ssh -i id_rsa user@jh2i.com -p 50004`<br>
> Given file: [id_rsa](/files/id_rsa)

Entering the line `ssh -i id_rsa user@jh2i.com -p 50004` with the identity file `id_rsa` I was able to get into the system, but I could not do much as the permission for `id_rsa`, file with private key for `ssh`, in my system was not what was expected. I tried multiple combinations for the expected correct permission, then I finally found the one: 400. Then it was just about reading the contents of the flag file for the flag.

```
flag{dont_ever_forget_that_newline}
```


<hr>



# Steganography:
## Spy vs. Spy
> Antonio Prohías was a cartoonist known primarily as the creator of the satirical comic strip Spy vs. Spy for Mad magazine. It wasn't until after 1997 when the comics changed from black and white to full color.<br>
> Given image: [Spy vs. Spy](/files/spy_vs_spy.png)

It was quite an easy challenge. I simply used Stegsolve to see the given image in different bit planes. The flag could clearly be seen in each of RED plane 0, GREEN plane 0 and BLUE plane 0.
[Spy vs. Spy flag](files/spy_vs_spy_flag.bmp)

```
flag{two_MAD_spies}
```

<hr>

    
## Substitute Face:
> \:\rabbit: \:rabbit \:\rabbit:<br>
> Given file+Solution: [face.txt](files/face.txt)

The given file contains a line of emojis. I tried to understand the meaning of the emojis by writing the name/description of each of them as given in Discord. But it made no sense at all. Then I came across a site: [emojipedia](https://emojipedia.org) which had a good amount of details of the emojis. It even had the codepoints for the emojis. Thus, I searched for each of the emojis in the site like this: `https://emojipedia.org/emoji/<emoji-here>` and noted down the codepoints of the emojis I searched for. The codepoints were in the form `U+1F4xy`, i.e. only the '`xy`' part was different. So, I took out the '`xy`' part and converted it into text.

The '`xy`' part I was talking about:

```
73 6f 78 63 64 21 20 7a 75 6d 20 62 6a 62 20 6a 64 21 20 79 69 63 73 7b 77 75 72 6a 69 69 63 5f 6c 75 62 78 77 75 70 6a 7d
```

and the text converting the above values gave:

```
soxcd! zum bjb jd! yics{wurjiic_lubxwupj}
```

I used [boxentriq](https://boxentriq.com/) to identify the type of cipher, and it returned 'Monoalphabetic substitution' as the best match. But upon entering the text there, and auto-analyzing it, there were messy suggestions. So, I went for solving it manually, i.e. replacing the characters with their best matching substitutes:  [screenshot in boxentriq](files/substitute_face_solved.png)

And that was that! The text above meant:

```
great! you did it! flag{mozilla_codemoji}
```

Thus, the flag:

```
flag{mozilla_codemoji}
```
    
    
<hr>



# Miscellaneous:
## Pseudo:
> Someone here has special powers... but who? And how!?<br>
> Connect here:<br>
> `ssh -p 50014 user@jh2i.com` # password is '`userpass`'

```
flag{hmmm_that_could_be_a_sneaky_backdoor}
``` 
    
<hr>



# Scavenger Hunt:
## Hacker101 Discord:
   
I did not know how to solve the 'Scavenger Hunt' category until I discovered a flag while randomly going through channels in Hacker101 discord server. There was a flag in the description of `#iot-village` channel in discord. I copied this flag and pasted it in `Hacker101 Discord` challenge and the flag got accepted.

```
flag{IoT_village_FTW}
```

<hr>

The flags for a few others:

## _config.yml#35:

on the last line at:
https://github.com/Hacker0x01/hacker101/blob/master/_config.yml

```
flag{git_sh!t_d0ne}
```

<hr>


## Pentesters Unite:
> Hack2Learn

https://github.com/Hacker0x01/hacker101/commit/717281070979d2b32a1751643997e6411e6c0444

```
flag{hacker_powered_pentest}
```


For the two above:

[Screenshots](https://github.com/jarp01/CTF-Writeups/blob/master/HacktivityCon%20CTF%202020/files/_config.yml%2Bpentesters%20unite.png)

<hr>

## The Streamer:
> https://twitch.tv/

[HackerOne TV about section in Twitch](https://www.twitch.tv/hackeronetv/about)

```
flag{kappa_kappa_kappa}
```

<hr>


## Like & Subscribe:
> There's something about liking and subscribing on YouTube!

[Youtube's about section of HackerOne](https://www.youtube.com/c/HackerOneTV/about)

```
flag{did_you_like_and_subscribe}
```

<hr>


## One of us:
> https://media1.giphy.com/media/Ae7SI3LoPYj8Q/200.gif<br>
> Go back to where it all started.   

https://github.com/Hacker0x01/docs.hackerone.com/commit/a287c78e344d8195cf1f2ecc948b524cea6c7fd8

```
flag{0ne_0f_1337_us}
```

<hr>


## \<a href="in">:

Look at the 'About' section in LinkedIn, and click on 'See all':
https://www.linkedin.com/company/hackerone

[About section - LinkedIn](/files/LinkedIn.png)

```
flag{www_hackerone_com_careers}
```

<hr>

## The Hacker101:
> Is this CTF working?

I had found the flag for this one quite unexpectedly. I went to play [Hacker101 CTF](https://ctf.hacker101.com/ctf) to relax(lol) as I had not been able to find any more flags here. After some time I scrolled down to the end in Hacker101 CTF page, there was a flag! I tried this flag in several challenges in 'Scavenger Hunt' category and got it accepted in 'The Hacker101' challenge.

    
```
flag{hack_4ll_th3_th1gs}
```
