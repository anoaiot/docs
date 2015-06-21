# [IGN Arm](http://repo.informatika.lipi.go.id/arm/image/)

## Apa itu IGN ARM ?
lihat [IGNwiki](http://igos-nusantara.or.id/wiki/index.php?title=Halaman_Utama#IGOS_Nusantara_ARM)

> **IGN ARM** adalah distro **IGOS Nusantara** yang dikembangkan khusus untuk komputer dengan arsitektur ARM.

## Instalasi
1. unduh [image] (http://repo.informatika.lipi.go.id/arm/image/)
2. kemudian extract file yang telah di unduh dengan cara ketik di terminal
~~~bash
$ sudo tar xvfJ filename.tar.xz
~~~
3. siapkan micro sdcard dengan kapasitas minimal **8 GB**
4. masukan micro sdcard kedalam extention sdcard dan pasang di pc / laptop
5. deteksi device melalui terminal dengan perintah **dmesg** misalkan
**/dev/mmclbk0**
6. apabila sudah dipastikan device berada ketik diterminal
~~~bash
$ sudo dd bs=4MB if=folder/image/ignarm/berada of=/dev/microsd/berada
~~~
7. Proses selesai masukan sdcard yang sudah terinstalasi ign arm kedalam komputer berbasis ARM
8. **Boot**

# [IGNSDK IoT Runtime](https://github.com/anak10thn/ignsdk-iot)
IGNSDK IoT runtime merupakan perkakas yang memudahkan client apps library IGNSDK IoT ([Shark.io](npmjs.com/package/shark.io)) mengakses interface perangkat keras, sensor, sql, filesystem, dan etc, menggunakan javascript API.

## Arsitektur
![IGNSDK Arsitektur](https://raw.githubusercontent.com/ignsdk/doc.iot/master/img/ign-arch.png)

## Cara mengakses petunjuk penggunaan

pada terminal, ketik
~~~bash
# ignsdk -h
~~~

perintah memunculkan informasi sebagai berikut :
~~~bash
Usage: ignsdk-iot [options]
IGOS Nusantara Software Development Kit For IoT

Options:
  -v, --version                               Show version
  -p, --port <port>                           Setup websocket port
  -t, --target <all, public, set ip address>  Set IP target
  -n, --nodejs <nodejs script>                Execute nodejs script
  -h, --help                                  Displays this help.
~~~

## Menjalankan runtime di jaringan lokal maupun public

pada terminal ketik

~~~bash
$ su
# ignsdk-iot -t all &
~~~

perintah tersebut untuk menjalankan runtime ignsdk-iot dengan mengarahkan ke IP yang tersedia pada device.

 **-t** itu menunjukan alamat **IP** yang akan menjalankan ignsdk-iot

jika berhasil outputnya akan menjadi :

~~~bash
# [1] 458
Server ON :  "0.0.0.0" Port : 6969
~~~

## Menjalankan NodeJS Script dengan runtime **ignsdk-iot**

~~~bash
$ su
# ignsdk-iot -n (aplikasi berbasis node js yang ingin dijalankan)
~~~

# Shark.io
JavaScript Client Library untuk mengakses API IGNSDK IoT. Saat ini shark.io baru dapat digunakan pada :
* NodeJS/JX Core
* HTML5

## Instalasi
```
$ npm install shark.io
```

## PIN Map
### Raspberry Pi 2
![](https://cloud.githubusercontent.com/assets/828293/7487407/2c1bc186-f3e1-11e4-91ad-575fc569055b.png)
source : http://www.element14.com/community/docs/DOC-73950/l/raspberry-pi-2-model-b-gpio-40-pin-block-pinout

## HTML5 Examples

Source : `tank-web-control.html`

![tank](https://github.com/ignsdk/doc.iot/raw/master/img/use/tank.gif)

~~~html
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
        <script type="text/javascript" src="../lib.js"></script>
        <script type="text/javascript">
            window.onload = function() {
                var socket;

                socket = new WebSocket("ws://192.168.1.164:6969");

                socket.onclose = function()
                {
                    console.error("web channel closed");
                };
                socket.onerror = function(error)
                {
                    console.error("web channel error: " + error);
                };
                socket.onopen = function()
                {
                    new sharkIO(socket, function(channel) {
                        window.fs = channel.objects.fs;
                        window.gpio = channel.objects.gpio;
                        gpio.set(18);
    			gpio.mode("out");
    			gpio.set(23);
    			gpio.mode("out");
    			gpio.set(24);
    			gpio.mode("out");
    			gpio.set(25);
    			gpio.mode("out");
                    });
                }
            }

            function maju(){
                reset()
                gpio.write(18,1);
                gpio.write(24,1);
            }
            function mundur(){
                reset()
                gpio.write(23,1);
                gpio.write(25,1);
            }
            function kanan_atas(){
                reset()
                gpio.write(18,1);
            }
            function kiri_atas(){
                reset()
                gpio.write(24,1);
            }
            function kanan_bawah(){
                reset()
                gpio.write(23,1);
            }
            function kiri_bawah(){
                reset()
                gpio.write(25,1);
            }
	    function reset(){
		  gpio.write(18,0);
		  gpio.write(23,0);
		  gpio.write(24,0);
		  gpio.write(25,0);
	    }
        </script>
    </head>
	<style>
	@media (min-width: 30em) {
    		.row { width: 100%; display: table; table-layout: fixed; }
    		.col { display: table-cell; }
	}
    button{
        display: block; width: 100%; padding: 16% 0;
    }
	</style>
    <body>
	<div class="row">
        <div class="col"></div>
        <div class="col"><button onclick="maju()"><h1>MAJU</h1></button></div>
        <div class="col"></div>
    </div>
    <div class="row">
        <div class="col"><button onclick="kiri_atas()"><h1>KIRI</h1></button></div>
        <div class="col"><button onclick="reset()"><h1>STOP</h1></button></div>
        <div class="col"><button onclick="kanan_atas()"><h1>KANAN</h1></button></div>
    </div>
    <div class="row">
        <div class="col"></div>
        <div class="col"><button onclick="mundur()"><h1>MUNDUR</h1></button></div>
        <div class="col"></div>
    </div>
    </body>
</html>
~~~


## NodeJS Examples

Source : `simple.js`
~~~javascript
'use strict';

var shark = require('shark.io');

shark.init('127.0.0.1:6969');
var setup = shark.setup;

setup.on('open',function(event){
    event.serial.info(function(data){
        console.log(data);
        process.exit(1);
    });
});
~~~

Source : `loop.js`
~~~javascript
'use strict';

var shark = require('shark.io');

shark.init('127.0.0.1:6969');
var loop = shark.loop;

function act(event){
    console.log("Running...");
}

loop(act,2000);
~~~

Source : `led_blink.js`

~~~javascript
'use strict';

var shark = require('shark.io');
var sleep = require('sleep');

shark.init('127.0.0.1:6969');
var loop = shark.loop;
var gpio;
shark.setup.on('open',function(event){
    gpio = event.gpio;
    gpio.set(18);
    gpio.mode("out");
});

function act(event){
    console.log("on");
    gpio.write(18,1);
    sleep.sleep(3);
    console.log("off");
    gpio.write(18,0);
}

loop(act,500);
~~~

Source : `gpio_read.js`
~~~javascript
'use strict';

var shark = require('shark.io');
var sleep = require('sleep');

shark.init('127.0.0.1:6969');
var loop = shark.loop;
var gpio;
shark.setup.on('open',function(event){
    gpio = event.gpio;
    gpio.set(18);
    gpio.mode("in");
    gpio.read(18,function(out){
       out.stream.connect(function(data){
          if(data == 1){
             console.log("ON")
          }
       });
    });
});
~~~

# Contributor
## Documentation
* Brahmanggi Aditya <brahmanggi@gmail.com>

## Web
* Rizky Ariestiyansyah <ariestiyansyah.rizky@gmail.com>
