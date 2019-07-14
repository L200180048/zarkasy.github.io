Date: 2019-07-12 10:56
Title: Alur Janus
Category: Janus

Salah satu hal terpenting dari sebuah software adalah dokumentasi, mungkin bisa dibilang hal kedua terpenting setelah software itu sendiri, karena tanpa dokumentasi yang baik, software tersebut akan susah untuk digunakan. Hal ini terjadi dengan janus, janus ini sempat saya singgung di artikel sebelumnya, yaitu webrtc server. Janus sebagai open source hanya dikembangkan oleh beberapa orang saja, mungkin hal inilah yang menyebabkan rendahnya kualitas dari dokumentasinya. Pengalamanku memakai janus, butuh hampir tiga hari untuk bisa mengerti bagaimana alur kerjanya, dan aku harus bolak-balik baca dokumentasi dan source code, nyoba jalanin program sendiri untuk bisa mengerti alur janus ini seperti apa. Kenapa hal ini bisa terjadi dengan janus? Jawabannya adalah karena pengembang software ini tidak memberikan contoh yang jelas didalam dokumentasinya, namun contoh alur coding ditaruh didalam source code demo, jadi kita harus mengerti bagaimana demo itu berjalan, selain itu juga kita harus membaca dokumentasi yang tidak utuh tersebut. 

Tapi alhamdulillah setelah beberapa hari mencoba, akhirnya aku nemu juga dokumentasi yang memberi pencerahan. Bagi yang sedang belajar janus, silahkan lihat pada bagian ini:

> The idea behind it's usage is the following:
>
> 1. you use attach() to create a Handle object;
> 2. in the success callback, your application logic can kick in: you may want to send a message to the plugin (send({msg})), negotiate a PeerConnection with the plugin right away ( createOffer followed by a send({msg, jsep})) or wait for something to happen to do anything;
> 3. the onmessage callback tells you when you've got messages from the plugin; if the jsep parameter is not null, just pass it to the library, which will take care of it for you; if it's an OFFER use createAnswer (followed by a send({msg, jsep}) to close the loop with the plugin), otherwise use handleRemoteJsep ;
> 4. whether you took the initiative to set up a PeerConnection or the plugin did, the onlocalstream and/or the onremotestream callbacks will provide you with a stream you can display in your page;
> 5. each plugin may allow you to manipulate what should flow through the PeerConnection channel: the send method and onmessage callback will allow you to handle this interaction (e.g., to tell the plugin to mute your stream, or to be notified about someone joining a virtual room), while the ondata callback is triggered whenever data is received on the Data Channel, if available (and the ondataopen callback will tell you when a Data Channel is actually available)
