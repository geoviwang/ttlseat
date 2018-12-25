<template>
  <div class="container">
    <br />
    <div class="col-fixed">
    <div class="row">
      <div class="col-4">
          <div class="row">
            <div id="wait1" class="seat" :class="seatClass.wait1" @click="upNdown"></div>
            <div id="wait2" class="seat" :class="seatClass.wait2" @click="upNdown"></div>
            <div id="wait3" class="seat" :class="seatClass.wait3" @click="upNdown"></div>
          </div>
          <br />
          <br />
          <br />
          <div class="row">
            <div id="wait4" class="seat" :class="seatClass.wait4" @click="upNdown"></div>
            <div id="wait5" class="seat" :class="seatClass.wait5" @click="upNdown"></div>
            <div id="wait6" class="seat" :class="seatClass.wait6" @click="upNdown"></div>
          </div>
      </div>
      <div class="col">
        <div class="row">
          <div class="col-1">
            <div id="seat1" class="row seat" :class="seatClass.seat1" @click="upNdown"></div>
            <div id="seat2" class="row seat" :class="seatClass.seat2" @click="upNdown"></div>
            <div id="seat3" class="row seat" :class="seatClass.seat3" @click="upNdown"></div>
            <div id="seat4" class="row seat" :class="seatClass.seat4" @click="upNdown"></div>
          </div>
          <div class="col-6">
            <div class="row table" v-on:click="admin"></div>
            <div class="row" style="margin: 0 auto;">
              <div id="seat5" class="seat" :class="seatClass.seat5" @click="upNdown"></div>
              <div id="seat6" class="seat" :class="seatClass.seat6" @click="upNdown"></div>
              <div id="seat7" class="seat" :class="seatClass.seat7" @click="upNdown"></div>
              <div id="seat8" class="seat" :class="seatClass.seat8" @click="upNdown"></div>
              <div id="seat9" class="seat" :class="seatClass.seat9" @click="upNdown"></div>
              <div id="seat10" class="seat" :class="seatClass.seat10" @click="upNdown"></div>
              <div id="seat11" class="seat" :class="seatClass.seat11" @click="upNdown"></div>
              <div id="seat12" class="seat" :class="seatClass.seat12" @click="upNdown"></div>
            </div>
          </div>
          <div class="">
            <div id="seat13" class="row seat" :class="seatClass.seat13" @click="upNdown"></div>
            <div id="seat14" class="row seat" :class="seatClass.seat14" @click="upNdown"></div>
            <div id="seat15" class="row seat" :class="seatClass.seat15" @click="upNdown"></div>
            <div id="seat16" class="row seat" :class="seatClass.seat16" @click="upNdown"></div>
          </div>
        </div>
      </div>
    </div>
    </div>
  </div>
</template>

<script>

import * as firebase from "firebase";
import $ from "jquery";
import moment from "moment";
moment.locale("zh-tw");

var config = {
    apiKey: "AIzaSyDOfQKzA2WKr50Rc1fbaVWpgAaW1ALXCSo",
    authDomain: "ttlseatdatabase.firebaseapp.com",
    databaseURL: "https://ttlseatdatabase.firebaseio.com",
    projectId: "ttlseatdatabase",
    storageBucket: "ttlseatdatabase.appspot.com",
    messagingSenderId: "775630335713"
  };
firebase.initializeApp(config);

firebase.auth().signInAnonymously().catch(function(error) {
  // Handle Errors here.
  var errorCode = error.code;
  var errorMessage = error.message;
  console.log(errorCode);
  console.log(errorMessage);
});

const db = firebase.database();

export default {
   name: 'QuerySeat',
   data() {
      return {
         adminCount: 0,
         seatClass:{
            'seat1': 'empty',
            'seat2': 'empty',
            'seat3': 'empty',
            'seat4': 'empty',
            'seat5': 'empty',
            'seat6': 'empty',
            'seat7': 'empty',
            'seat8': 'empty',
            'seat9': 'empty',
            'seat10': 'empty',
            'seat11': 'empty',
            'seat12': 'empty',
            'seat13': 'empty',
            'seat14': 'empty',
            'seat15': 'empty',
            'seat16': 'empty',
            'wait1': 'empty',
            'wait2': 'empty',
            'wait3': 'empty',
            'wait4': 'empty',
            'wait5': 'empty',
            'wait6': 'empty'
         }
      }
   },
   methods: {
      upNdown: function(el) {
         if(this.adminCount < 5) return;
         var id = el.target.id;
         var seatClass = this.seatClass;
         if(seatClass[id] == 'empty') {
            db.ref('/seat/' + id).set({
               people: 'arrival'
            });
            setTimeout(function(){
                db.ref('/seat/' + id).set({
                   people: 'awhile'
                });
            }, 10000);
         } else {
            db.ref('/seat/' + id).set({
               people: 'empty'
            });
         }
      },
      admin: function() {
         this.adminCount++;
         if(this.adminCount == 5) {
            alert('安安>.^');
         }
      }
   },
   mounted() {
      var sClass = this.seatClass;
      db.ref('/seat/').on("value", function(snapshot) {
      var data = snapshot.val()
      for(var seat in data) {
         sClass[seat] = data[seat].people;
      }
    });
   }
}
</script>

<style scoped>
.seat {
    border: 3px solid;
    border-radius: 100%;
    width: 40px;
    height: 40px;
}
.empty {
    background-color: blue;
}
.arrival {
    background-color: red;
    animation-name: oxxo;
    animation-duration:2s;
    animation-iteration-count: infinite;
}
.awhile {
    background-color: red;
}

@keyframes oxxo{
   0%{
     background: red;
   }
   50%{
     background: black;
   }
   100%{
     background: red;
   }
}
.table {
    /*background-color: red;*/
    border: 3px solid;
    width: 100%;
    height: 172px;
}
.col-fixed {
  width: 1200px;
}
</style>
