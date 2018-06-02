# Zencash on Tor

### Linux

#### Install Tor from the official repository
First add the Tor repository to your package sources
```
sudo su -c "echo 'deb http://deb.torproject.org/torproject.org '$(lsb_release -c | cut -f2)' main' > /etc/apt/sources.list.d/torproject.list"
gpg --keyserver keys.gnupg.net --recv A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89
gpg --export A3C4F0F979CAA22CDBA8F512EE8CBC9E886DDD89 | sudo apt-key add -
```
and install it
```
sudo apt-get update
sudo apt-get install tor deb.torproject.org-keyring
```
then add your current user to the `debian-tor` group to be able to use cookie authentication.
```
sudo usermod -a -G debian-tor $(whoami)
```

Now log out and back in, then edit `/etc/tor/torrc` to enable the control port, enable cookie authentication and make the auth file group readable.
```
sudo sed -i 's/#ControlPort 9051/ControlPort 9051/g' /etc/tor/torrc
sudo sed -i 's/#CookieAuthentication 1/CookieAuthentication 1/g' /etc/tor/torrc
sudo su -c "echo 'CookieAuthFileGroupReadable 1' >> /etc/tor/torrc"
sudo su -c "echo 'LongLivedPorts 9033' >> /etc/tor/torrc"
```
Now restart the Tor service.
```
sudo systemctl restart tor.service
```

#### Setting up zend to be reachable by other Tor nodes

If you've configured Tor as previously described there is nothing more you need to do. When you start zend without any command line options e.g. `./zend` it will automatically create a HiddenService and be reachable via the Tor network and clearnet. The node should have created a file `~/.zen/onion_private_key`, this file stores the private key of your HiddenService address.

When you use `./zen-cli getnetworkinfo` you should see that your node is reachable as a HiddenService like so:
```
[...]
    {
      "name": "onion",
      "limited": false,
      "reachable": true,
      "proxy": "127.0.0.1:9050",
      "proxy_randomize_credentials": true
    }
  ],
  "relayfee": 0.00000100,
  "localaddresses": [
    {
      "address": "lbfuusf2bg5e2t3j.onion",
      "port": 9033,
      "score": 4
    }
[...]
```

You can now give out your onion address, nodes will then be able to connect to it :D

#### Connect to Tor nodes only:
edit your zen.conf and add
```
proxy=127.0.0.1:9050
onlynet=tor
addnode=664sm6tboxgulaar.onion
addnode=k6yjiqxfehnbey5x.onion
addnode=ktp7b3ffc324zeoq.onion
addnode=k4mndsz24sj2fk7w.onion
addnode=52ywlur6mlmpl62j.onion
addnode=e5nntkmas4nxxhxd.onion
addnode=ifmrspt373jdl6b6.onion
addnode=4mt3rihnc6jmud3b.onion
addnode=mdquqngm2zrgkl37.onion
addnode=xht6hfirwgrsiwob.onion
addnode=r55o3d2k2adg77ua.onion
addnode=fydtl3c3mog4zbdp.onion
addnode=5bbzenaugfyys7mz.onion
addnode=issfdkq2jj5ljg5f.onion
addnode=c3hdrvp6tkaq4eaw.onion
addnode=kzup5swqhk24vkzc.onion
addnode=eahbq2et2yt5ayoy.onion
addnode=zqrx7t7ajtltdn7j.onion
addnode=k5qqpbnxctcv7lo6.onion
addnode=icwop6z3yekcmplk.onion
addnode=qy5qyqi6dvcvlfyk.onion
addnode=chy27pne6xjszsyl.onion
addnode=jdbffgdgebo3m56g.onion
addnode=fwjflk4cimeftuhi.onion
addnode=xkrx5m4jqyzwydky.onion
addnode=twhb7td2f7oqdnm3.onion
addnode=stgdahue6pvr2guq.onion
addnode=qu6p6347mfvpprbw.onion
addnode=u7hauzipggwtbqqx.onion
addnode=xy7dymivxqtkqg4o.onion
addnode=62octnztu77js3ej.onion
addnode=tigybqpyg3zysm6v.onion
addnode=7luj6fnpr5ilmj5d.onion
addnode=md344v42dm6rd6ay.onion
addnode=caafwewwghymptue.onion
addnode=qxpwiaar4l6rvz3h.onion
addnode=r6exvwywoqyn6op3.onion
addnode=pza5fqmdl3zu32cu.onion
addnode=etskzar66wheksdd.onion
addnode=pqbjp4yco7p5pnpk.onion
addnode=bee4bcaxsg3637xc.onion
addnode=yylmbfsnavhmq5eh.onion
addnode=4rhhb2l37jerpxfh.onion
addnode=qr6dvzrz3g6a6p4e.onion
addnode=v7mqyhrdxb2bqgze.onion
addnode=qg4guuwggvbyjigw.onion
addnode=eorrku3hauy53zup.onion
addnode=xqrvu4rxw7pulgb3.onion
addnode=mbkpyfwjudi423xp.onion
addnode=vxp6kyw6hhjzu7r2.onion
addnode=ayeypndttmb54eeu.onion
addnode=wchizsqjxr3vtmm6.onion
addnode=bdfdc3ch5feattda.onion
addnode=gbqx534g4it22bj6.onion
addnode=qkdumxh56iyxlh64.onion
addnode=ja3dmlnvmxvddqiv.onion
addnode=bibjccpeo4ynsvwk.onion
addnode=hk5bgro4r4du54ig.onion
addnode=btt45hsebudhuzre.onion
addnode=fq3yhrgugsd4mddb.onion
addnode=6noiyva65ujhkvkr.onion
addnode=7pe25co6imeqtwvd.onion
addnode=xn2i64vmokankqo2.onion
addnode=nlqewns33li7piel.onion
addnode=ihzm2thdzhnunzo3.onion
addnode=hl6dkcnla7pcxoww.onion
addnode=zr4pevx3fiicaiwj.onion
addnode=zibr562qgvo3ytsv.onion
addnode=y4gebfj7vahp2hfi.onion
addnode=vrghwxmuvbdq5yzf.onion
addnode=ruiiadphma4sade3.onion
addnode=hfcq7x6m34qkhcqr.onion
addnode=iewzdrijtabs67ws.onion
addnode=gvvktmsjoonhartd.onion
addnode=hje3mngtjo7rrvks.onion
addnode=k7uyp756k4ii2zjx.onion
addnode=yrpfged3ysux7rab.onion
addnode=u3rrn4mvgdovr53z.onion
addnode=sjo576gsfwttup7a.onion
addnode=urv2rsuhys2hxnux.onion
addnode=c5dsmhsnfnfvjkss.onion
addnode=rcyl6vka36c6vw6t.onion
addnode=lfdcgiyzmsmpaemv.onion
addnode=dnurlt2wojgahd6y.onion
``` 

Restart zend and your node will officially be hidden and outta sight :D

### Windows

#### Install and configure Tor

Download the Tor expert bundle for Windows from `https://www.torproject.org/download/download`and extract the zip file to a subfolder.

Now create a new folder at `%APPDATA%\tor` and create a new text file `%APPDATA%\tor\torrc` and put this in it (note that the file needs to be saved without a `.txt` extension):
```
ControlPort 9051
CookieAuthentication 1
LongLivedPorts 9033
```

Now open a command prompt and change to the directory you extracted Tor to e.g.
```
cd c:\Downloads\tor-win32-0.3.0.10
```
and start tor.exe with
```
Tor\tor.exe
```
you should see Tor's log output in the command prompt window.

#### Setting up zend to be reachable by other Tor nodes

Same as the Linux guide but use `.\zend.exe`, `.\zen-cli.exe getnetworkinfo` and `%APPDATA%\Zen\onion_private_key`.

#### Connect to Tor nodes only:

Same as the Linux guide but edit the config at `%APPDATA%\Zen\zen.conf`.

### List of Tor nodes:
```
proxy=127.0.0.1:9050
onlynet=tor
addnode=664sm6tboxgulaar.onion
addnode=k6yjiqxfehnbey5x.onion
addnode=ktp7b3ffc324zeoq.onion
addnode=k4mndsz24sj2fk7w.onion
addnode=52ywlur6mlmpl62j.onion
addnode=e5nntkmas4nxxhxd.onion
addnode=ifmrspt373jdl6b6.onion
addnode=4mt3rihnc6jmud3b.onion
addnode=mdquqngm2zrgkl37.onion
addnode=xht6hfirwgrsiwob.onion
addnode=r55o3d2k2adg77ua.onion
addnode=fydtl3c3mog4zbdp.onion
addnode=5bbzenaugfyys7mz.onion
addnode=issfdkq2jj5ljg5f.onion
addnode=c3hdrvp6tkaq4eaw.onion
addnode=kzup5swqhk24vkzc.onion
addnode=eahbq2et2yt5ayoy.onion
addnode=zqrx7t7ajtltdn7j.onion
addnode=k5qqpbnxctcv7lo6.onion
addnode=icwop6z3yekcmplk.onion
addnode=qy5qyqi6dvcvlfyk.onion
addnode=chy27pne6xjszsyl.onion
addnode=jdbffgdgebo3m56g.onion
addnode=fwjflk4cimeftuhi.onion
addnode=xkrx5m4jqyzwydky.onion
addnode=twhb7td2f7oqdnm3.onion
addnode=stgdahue6pvr2guq.onion
addnode=qu6p6347mfvpprbw.onion
addnode=u7hauzipggwtbqqx.onion
addnode=xy7dymivxqtkqg4o.onion
addnode=62octnztu77js3ej.onion
addnode=tigybqpyg3zysm6v.onion
addnode=7luj6fnpr5ilmj5d.onion
addnode=md344v42dm6rd6ay.onion
addnode=caafwewwghymptue.onion
addnode=qxpwiaar4l6rvz3h.onion
addnode=r6exvwywoqyn6op3.onion
addnode=pza5fqmdl3zu32cu.onion
addnode=etskzar66wheksdd.onion
addnode=pqbjp4yco7p5pnpk.onion
addnode=bee4bcaxsg3637xc.onion
addnode=yylmbfsnavhmq5eh.onion
addnode=4rhhb2l37jerpxfh.onion
addnode=qr6dvzrz3g6a6p4e.onion
addnode=v7mqyhrdxb2bqgze.onion
addnode=qg4guuwggvbyjigw.onion
addnode=eorrku3hauy53zup.onion
addnode=xqrvu4rxw7pulgb3.onion
addnode=mbkpyfwjudi423xp.onion
addnode=vxp6kyw6hhjzu7r2.onion
addnode=ayeypndttmb54eeu.onion
addnode=wchizsqjxr3vtmm6.onion
addnode=bdfdc3ch5feattda.onion
addnode=gbqx534g4it22bj6.onion
```

Submit a PR to have yours added!
