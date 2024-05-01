<template>
  <v-app>
    <v-app-bar color="dark-white" dark max-height="70">
      <v-toolbar-title>User</v-toolbar-title><v-spacer></v-spacer>
      <v-btn color="primary" to="/">Log Out</v-btn>
    </v-app-bar>
    <v-navigation-drawer app>
      <v-divider length="0">h</v-divider>

      <v-list dense nav>
        <img src="@/assets/sona.png" alt="" width="230" height="140" />

        <v-divider></v-divider>

        <v-list-item v-for="item in items" :key="item.title" :to="item.to" link>
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title style="text-align: left; font-weight: bold"
              >{{ item.title }}
            </v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-container fluid>
      <v-row dense>
        <v-col
          v-for="(card, index) in cards"
          :key="card.title"
          :cols="card.flex"
        >
          <v-hover v-slot="{ hover }" open-delay="200">
            <v-card
              :elevation="hover ? 16 : 2"
              :class="{ 'on-hover': hover }"
              class="mx-auto"
            >
              <v-img
                :src="card.src"
                class="white--text align-end"
                gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                height="200px"
              >
                <v-card-title :inner-text.prop="card.title"></v-card-title>
              </v-img>

              <v-card-actions>
                <!-- <v-btn dark  @click="buttonClicked(index)"> Open </v-btn> -->

                <v-dialog
                  v-model="dialog1"
                  persistent
                  max-width="600px"
                  :retain-focus="false"
                >
                  <template v-slot:activator="{ on, attrs }">
                    <v-btn
                      dark
                      v-bind="attrs"
                      v-on="on"
                      @click="buttonClicked(index, card)"
                    >
                      Open
                    </v-btn>
                  </template>
                  <v-card>
                    <v-card-title>
                      <!-- <span class="text-h5">Admin Form</span> -->
                    </v-card-title>
                    <v-card-text>
                      <v-container>
                        <v-row>
                          <v-col cols="12">
                            <h1>{{ samG }}</h1>
                          </v-col>
                          <v-row>
                            <div class="text-overline mb-1">
                              Enter Details of Part Number
                            </div>
                          </v-row>
                          <v-row>
                            <v-col>
                              <!-- <div v-if=this.polyarr[0].alphabetical> -->
                              <div v-for="index in count" :key="index">
                                <v-text-field
                                  label="Enter text"
                                  v-model="textarray[Path[index - 1]]"
                                  solo
                                  outlined
                                  dense
                                  :rules="filteredRules"
                                  type="text"
                                  @click="textclicked(index)"
                                  maxlength="5"
                                  clearable
                                  v-if="isDisabledsss"
                                >
                                </v-text-field>
                              </div>

                              <!-- </div> -->
                            </v-col>
                            <v-col>
                              <div v-for="index1 in checkcount" :key="index1">
                                <v-select
                                  v-model="lovs[CheckPath[index1 - 1]]"
                                  label="Choose an Option"
                                  :items="SamArr[index1 - 1]"
                                  dense
                                  solo
                                  v-if="isDisabledarr"
                                ></v-select>
                              </div>
                            </v-col>
                          </v-row>
                          <v-row>
                            <v-col>
                              <div
                                v-for="(i, index) in InputDataArr"
                                :key="index"
                              >
                                <v-text-field
                                  :label="i"
                                  v-model="inputsarray[index]"
                                  placeholder=""
                                  dense
                                  outlined
                                ></v-text-field>
                              </div>
                            </v-col>
                          </v-row>
                        </v-row>
                      </v-container>
                    </v-card-text>
                    <v-card-actions>
                      <v-spacer></v-spacer>
                      <v-btn
                        color="blue darken-1"
                        text
                        @click="(dialog1 = false), submit()"
                      >
                        Submit
                      </v-btn>
                      <v-btn text @click="dialog1 = false"> Cancel </v-btn>
                    </v-card-actions>
                  </v-card>
                </v-dialog>
              </v-card-actions>
            </v-card>
          </v-hover>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
/* eslint-disable */
import axios from "axios";
export default {
  data() {
    return {
      samG: "",
      lovs: [],
      textarray: [],
      click: false,
      ava: true,
      polyM: "",
      dig: [],
      year: "",
      day: "",
      month: "",
      time: "",
      Date: "",
      InputDataArr: [],
      nor: [],
      inputsarray: [],
      InputArr: [],
      InputArray: [],
      pra: "",
      checklength: {},
      count: null,
      checkcount: null,
      isDisabledsss: false,
      isDisabledarr: false,
      CheckPath: [],
      CheckPath1: [],
      mainindex: null,
      mainSeq: [],
      AllSeq: [],
      mainPolyObj: {},
      MainFinalString: {
        FinalString: "",
      },
      textindex: null,
      // sam: false,
      poly: [],
      realobject: {},
      polyarr: [],
      dialog1: false,
      CardData: {},
      textindex1: 0,
      resultdata: [],
      realdata: [],
      ifcon: false,
      SamArr: [],
      textlen: [],
      extrapolyarr: [],
      Path: [],
      rules: [
        (v) => /^[a-zA-Z]+$/.test(v) || "Only alphabets are allowed",
        (v) => /^[0-9]+$/.test(v) || "Only numbers are allowed",
        (v) => /^[\W]+$/.test(v) || "Only symbols are allowed",
      ],
      cards: [],
      transparent: "rgba(255, 255, 255, 0)",
      items: [{ title: "Forms", icon: "mdi-form-select", to: "/LoginPage" }],
    };
  },
  watch: {
    inputsarray() {
      
    },
    // textarray() {
    //   // 
    //   this.textarray = this.textarray.map((str) => str.toUpperCase());
    // },
    lovs() {
      
    },
  },
  mounted() {
    this.admindata();
    this.getdata();

    // this.ifcondition();
  },

  computed: {
    filteredRules() {
      if (
        this.extrapolyarr[this.textindex1].alphabetical &&
        !this.extrapolyarr[this.textindex1].numerical &&
        !this.extrapolyarr[this.textindex1].symbols
      ) {
        return [this.rules[0]];
      } else if (
        !this.extrapolyarr[this.textindex1].alphabetical &&
        this.extrapolyarr[this.textindex1].numerical &&
        !this.extrapolyarr[this.textindex1].symbols
      ) {
        return [this.rules[1]];
      } else if (
        !this.extrapolyarr[this.textindex1].alphabetical &&
        !this.extrapolyarr[this.textindex1].numerical &&
        this.extrapolyarr[this.textindex1].symbols
      ) {
        return [this.rules[2]];
      } else if (
        this.extrapolyarr[this.textindex1].alphabetical &&
        this.extrapolyarr[this.textindex1].numerical &&
        !this.extrapolyarr[this.textindex1].symbols
      ) {
        return [
          (v) =>
            /^[a-zA-Z0-9]+$/.test(v) ||
            "Only alphabets and numbers are allowed",
        ];
      } else if (
        this.extrapolyarr[this.textindex1].alphabetical &&
        !this.extrapolyarr[this.textindex1].numerical &&
        this.extrapolyarr[this.textindex1].symbols
      ) {
        return [
          (v) =>
            /^[a-zA-Z\W]+$/.test(v) || "Only alphabets and symbols are allowed",
        ];
      } else if (
        !this.extrapolyarr[this.textindex1].alphabetical &&
        this.extrapolyarr[this.textindex1].numerical &&
        this.extrapolyarr[this.textindex1].symbols
      ) {
        return [
          (v) => /^[0-9\W]+$/.test(v) || "Only numbers and symbols are allowed",
        ];
      } else if (
        this.extrapolyarr[this.textindex1].alphabetical &&
        this.extrapolyarr[this.textindex1].numerical &&
        this.extrapolyarr[this.textindex1].symbols
      ) {
        return [
          (v) =>
            /^[a-zA-Z0-9\W]+$/.test(v) ||
            "Only alphabets, numbers, and symbols are allowed",
        ];
      } else {
        return [];
      }
    },
  },

  methods: {
    textclicked(index) {
      this.textindex = index;
      
      this.textindex1 = this.textindex - 1;
    },

    // ifcondition(){

    //   if(this.polyarr[0].alphabetical){
    //     
    //   }
    //   else{
    //     
    //   }

    // },
    submit() {
      // this.InputArray = this.inputsarray;
      // this.InputArr.push(this.textarray);
      // this.InputArr.push(this.lovs);
      // this.InputArr.push(...this.InputArray);
      // this.InputArr.push(this.polyM);
      // 

      // 
      // 
      // 
      let len = this.mainSeq.length;
      

      let mainarray = new Array(len);

      if (this.Path.length) {
        // 

        for (let j = 0; j < this.Path.length; j++) {
          // 
          mainarray[this.Path[j]] = this.textarray[this.Path[j]];
        }
      }

      if (this.CheckPath.length) {
        // 
        for (let j = 0; j < this.CheckPath.length; j++) {
          // 
          mainarray[this.CheckPath[j]] = this.lovs[this.CheckPath[j]];
        }
      }

      //   for (const key in result) {
      //   if (result.hasOwnProperty(key)) {
      //     const value = result[key];
      //     const isInt = Number.isInteger(Number(value));
      //     if (isInt) {
      //       this.checklength[key] = value;
      //       
      //     }
      //   }
      // }

      let len1 = this.CardData[this.mainindex].sam.length - 1;
      let realobj = this.CardData[this.mainindex].sam[len1];

      //  

      for (let i = 0; i < this.mainSeq.length; i++) {
        if (mainarray[i]) {
          
        } else {
          if (this.mainSeq[i] === "prefix") {
            mainarray[i] = realobj[i];
            
          }
          if (this.mainSeq[i] === "suffix") {
            mainarray[i] = realobj[i];
            
          }
          if (this.mainSeq[i] === "text1") {
            mainarray[i] = realobj[i];
            
          }
          if (this.mainSeq[i] === "text2") {
            mainarray[i] = realobj[i];
            
          }
          if (this.mainSeq[i] === "text3") {
            mainarray[i] = realobj[i];
            
          }
          if (this.mainSeq[i] === "text4") {
            mainarray[i] = realobj[i];
            
          }
          if (this.mainSeq[i] === "text5") {
            mainarray[i] = realobj[i];
            
          }
          if (this.mainSeq[i] === "date") {
            mainarray[i] = this.Date;
            
          }
          if (this.mainSeq[i] === "day") {
            mainarray[i] = this.day;
            
          }
          if (this.mainSeq[i] === "month") {
            mainarray[i] = this.month;
            
          }
          if (this.mainSeq[i] === "time") {
            mainarray[i] = this.time;
            
          }
          if (this.mainSeq[i] === "year") {
            mainarray[i] = this.year;
            
          }
          if (this.mainSeq[i] === "sequence") {
            mainarray[i] = this.AllSeq.sequence;
            
          }
        }
      }
      

      let MainArray = "";
      for (let l = 0; l < mainarray.length; l++) {
        MainArray += mainarray[l];
      }
      

      this.MainFinalString.PartString = MainArray;
      this.MainFinalString.sequence = this.AllSeq.sequence;

      this.postdata();
      // 
    },

    async postdata() {
      await axios
        .post("http://localhost:8083/api/items7", this.MainFinalString)
        .then((result) => {
          // 
          // this.getdata();
          location.reload();
        })
        .catch((err) => {
          
        });
    },

    checklen(result) {
      // this.checklength.prefix = result.hasOwnProperty("prefix");
      // this.checklength.suffix = result.hasOwnProperty("suffix");
      // this.checklength.text1 = result.hasOwnProperty("text1");
      // this.checklength.text2 = result.hasOwnProperty("text2");
      // this.checklength.text3 = result.hasOwnProperty("text3");
      // this.checklength.text4 = result.hasOwnProperty("text4");
      // this.checklength.text5 = result.hasOwnProperty("text5");

      for (const key in result) {
        if (result.hasOwnProperty(key)) {
          const value = result[key];
          const isInt = Number.isInteger(Number(value));
          if (isInt) {
            this.checklength[key] = value;
            
          }
        }
      }
      delete this.checklength.sequence;
      for (const key in this.checklength) {
        this.textlen.push(this.checklength[key]);
      }
      this.textlen = this.textlen.map(Number);
      
    },

    cancel() {
      this.InputArray = [];
    },

    buttonClicked(index, card) {
      this.mainindex = index;
      let len1 = this.CardData[index].sam.length - 2;
      this.realobject = this.CardData[index].sam[len1];
      
      this.checklen(this.realobject);
      this.click = true;
      
      this.isDisabledsss = false;
      this.SamArr = [];
      this.checkcount = null;
      this.count = null;
      // 
      this.isDisabledarr = false;

      this.samG = this.cards[index].title;
      this.polyM = this.cards[index].partnumber;

      let polyobj = {
        alphabetical: false,
        numerical: false,
        symbols: false,
      };
      // index=index+1
      let i1 = this.CardData[index].sam.length - 1;
      // for (let i = 0; i < this.CardData[index].sam[i1].length; i++) {
      //   // 
      //   // 
      //   // this.nor = this.resultdata[index].UserData[i];

      //   // let hasArray = this.CardData[index].sam[i1][i];
      //   let normal = this.CardData[index].sam[i1][i];
      //   
      //   if (normal.includes("alphabetical")) {
      //     polyobj.alphabetical = true;
      //     
      //     break;
      //   }
      //   if (normal.includes("numerical")) {
      //     polyobj.numerical = true;
      //     break;
      //   }
      //   if (normal.includes("symbols")) {
      //     polyobj.symbols = true;
      //     break;
      //   }
      // }

      // let filteredStrings1 = this.CardData[index].sam[i1].filter((str) =>
      //   str.includes("alphabetical")
      // );
      // let filteredStrings2 = this.CardData[index].sam[i1].filter((str) =>
      //   str.includes("numerical")
      // );
      // let filteredStrings3 = this.CardData[index].sam[i1].filter((str) =>
      //   str.includes("symbols")
      // );

      

      // 
      // 
      // 
      let path = [];
      this.Path = [];
      for (let p = 0; p < this.CardData[index].sam[i1].length - 1; p++) {
        let polyobj = {
          alphabetical: false,
          numerical: false,
          symbols: false,
        };

        let filteredarr1 =
          this.CardData[index].sam[i1][p].includes("alphabetical");
        let filteredarr2 =
          this.CardData[index].sam[i1][p].includes("numerical");
        let filteredarr3 = this.CardData[index].sam[i1][p].includes("symbols");

        if (filteredarr1) {
          polyobj.alphabetical = true;
          
        }
        if (filteredarr2) {
          polyobj.numerical = true;
        }
        if (filteredarr3) {
          polyobj.symbols = true;
        }

        if (filteredarr1 || filteredarr2 || filteredarr3) {
          this.polyarr.push(polyobj);
          path.push(p);
        }
      }
      this.Path = path;

      this.extrapolyarr = this.polyarr;
      this.count = this.Path.length;
      
      // if (filteredStrings1.length) {
      //   polyobj.alphabetical = true;
      // } else if (filteredStrings2.length) {
      //   polyobj.numerical = true;
      // } else if (filteredStrings3.length) {
      //   polyobj.symbols = true;
      // }
      // 
      // 
      // 
      polyobj = {
        alphabetical: false,
        numerical: true,
        symbols: false,
      };
      this.mainPolyObj = polyobj;
      // let common = filteredStrings1.filter((item) =>
      //   filteredStrings2.includes(item)
      // );
      // let common1 = filteredStrings2.filter((item) =>
      //   filteredStrings3.includes(item)
      // );
      // let common3 = filteredStrings1.filter((item) =>
      //   filteredStrings3.includes(item)
      // );

      // 
      // 
      // 

      // const greatest = Math.max(
      //   filteredStrings1.length,
      //   filteredStrings2.length,
      //   filteredStrings3.length
      // );

      // const num1 = filteredStrings1.length;
      // const num2 = filteredStrings2.length;
      // const num3 = filteredStrings3.length;

      // let a1 = false;
      // let a2 = false;
      // let a3 = false;

      // if (num1 >= num2) {
      //   if (num1 >= num3) {
      //     // 
      //     this.count = num1;
      //     a1 = true;
      //   } else {
      //     this.count = num3;
      //     a3 = true;
      //     // 
      //   }
      // } else {
      //   if (num2 >= num3) {
      //     this.count = num2;
      //     a2 = true;
      //     // 
      //   } else {
      //     this.count = num3;
      //     a3 = true;
      //     // 
      //   }
      // }
      // let path = [];
      // this.Path = [];
      // if (a1 == true) {
      //   for (let k = 0; k < filteredStrings1.length; k++) {
      //     const index1 = this.CardData[index].sam[i1].indexOf(
      //       filteredStrings1[k]
      //     );
      //     path.push(index1);
      //   }
      // }
      // if (a2 == true) {
      //   for (let k = 0; k < filteredStrings2.length; k++) {
      //     const index1 = this.CardData[index].sam[i1].indexOf(
      //       filteredStrings2[k]
      //     );
      //     path.push(index1);
      //   }
      // }
      // if (a3 == true) {
      //   for (let k = 0; k < filteredStrings3.length; k++) {
      //     const index1 = this.CardData[index].sam[i1].indexOf(
      //       filteredStrings3[k]
      //     );
      //     path.push(index1);
      //   }
      // }
      
      // this.Path = path;

      // this.count = greatest;

      // const notCommonValues = filteredStrings1.filter(value => !filteredStrings2.includes(value) && !filteredStrings3.includes(value))
      //   .concat(filteredStrings2.filter(value => !filteredStrings1.includes(value) && !filteredStrings3.includes(value)))
      //   .concat(filteredStrings3.filter(value => !filteredStrings3.includes(value) && !filteredStrings2.includes(value)));

      // const common = filteredStrings1.filter(item => filteredStrings2.includes(item))

      // // Remove the common elements from the arrays
      // const arr1WithoutCommon = filteredStrings1.filter(item => !common.includes(item))
      // const arr2WithoutCommon = filteredStrings2.filter(item => !common.includes(item))

      // // Combine the remaining elements into a single array
      // const combined = [...arr1WithoutCommon, ...arr2WithoutCommon]

      // 
      // 

      // this.polyarr.push(polyobj);

      // this.checkcondition(this.polyarr,index)
      // for(let i=0;i<this.polyarr.length;i++){

      // }
      // if(this.polyarr[index].symbols ){
      //   
      //   this.isDisabledsss=true;
      // }
      // if(this.polyarr[index].alphabetical){
      //   
      //   this.isDisabled=true;
      // }
      // if(this.polyarr[index].numerical){
      //   
      //   this.isDisabled=true;
      // }

      
      let len4 = this.CardData[index].sam.length - 2;
      let allseq = this.CardData[index].sam[len4];
      // 
      // 
      let sequenced = [];
      sequenced = allseq.seq;
      delete allseq.seq;
      
      
      this.mainSeq = [];
      this.AllSeq = [];
      this.mainSeq = sequenced;
      this.AllSeq = allseq;
      //     for (i = 0; i < seq.length; i++) {
      //       if (seq[i] === 'prefix') {
      //         if (this.CardData[index].sam[i][0].contains('alphabetical') || this.CardData[index].sam[i][0].contains('numerical') || this.CardData[index].sam[i][0].contains('symbols')) {
      //           this.ans.push(this.textarray[i]);
      //           break;
      //       }
      //       // else if(this.CardData[index].sam[i][0]==='lovs1'){

      //       // }

      //         else {
      //           this.ans.push(this.CardData[index].sam[i][i]);
      //         }
      //     } else if(seq[i] === 'suffix'){
      //       if(this.CardData[index].sam[i][i].contains('alphabetical') || this.CardData[index].sam[i][i].contains('numerical') || this.CardData[index].sam[i][i].contains('symbols')){
      //         this.ans.push(this.textarray);
      //         break;
      //       }
      //     }

      // };

      this.Date = null;
      this.time = null;
      this.day = null;
      this.month = null;
      this.year = null;
      this.finalDate(allseq.date);
      this.finalDay(allseq.day);
      this.finalMonth(allseq.month);
      this.finalTime(allseq.time);
      this.finalYear(allseq.year);

      
      
      
      

      this.InputDataArr = [];
      let len = this.CardData[index].sam.length - 2;
      for (let i = 2; i < len; i++) {
        this.InputDataArr.push(this.CardData[index].sam[i]);
      }
      if (this.polyarr[0].symbols) {
        // 
        this.isDisabledsss = true;
      } else if (this.polyarr[0].alphabetical) {
        // 
        this.isDisabledsss = true;
      } else if (this.polyarr[0].numerical) {
        // 
        this.isDisabledsss = true;
      }
      this.polyarr = [];
      // 
      this.checkforcheckbox(index);
      // 
      this.checklength = {};
      this.textlen = [];
      // this.submitpart();
    },

    checkforcheckbox(index) {
      let i2 = this.CardData[index].sam.length - 1;
      // let hasArray = this.CardData[index].sam[i2].some(Array.isArray);
      // // let hasArray = this.CardData[index].sam;
      // 
      // if (hasArray) {
      //   let ind = this.CardData[index].sam[i].findIndex(Array.isArray);
      //   this.SamArr = this.CardData[index].sam[i][ind];
      //   
      //   this.isDisabledarr = true;
      // }

      let count = 0;
      let checkpath = [];
      this.CheckPath = [];

      for (let i = 0; i <= i2; i++) {
        if (Array.isArray(this.CardData[index].sam[i2][i])) {
          this.SamArr.push(this.CardData[index].sam[i2][i]);
          checkpath.push(i);
          count++;
        }
      }

      this.CheckPath = checkpath;
      // this.CheckPath1=this.CheckPath

      

      if (this.SamArr.length) {
        this.isDisabledarr = true;
        this.checkcount = count;
      }

      // 

      // if()
    },

    //  checkcondition(con,index){
    //   // if(this.con[index].symbols ){
    //   //       
    //   //       this.isDisabledsss=true;
    //   //     }
    //       // if(this.polyarr[index].alphabetical){
    //       //   
    //       //   this.isDisabledsss=true;
    //       // }
    //       // if(this.polyarr[index].numerical){
    //       //   
    //       //   this.isDisabledsss=true;
    //       // }
    //  },

    async getdata() {
      axios
        .get("http://localhost:8083/api/items2")
        .then((result) => {
          this.resultdata = result.data;
          
        })
        .catch((err) => {
          
        });

      // axios
      // .get("http://localhost:8083/api/items6")
      // .then((result) => {
      //   this.realdata = result.data;
      //   
      // })
      // .catch((err) => {
      //   
      // });
    },

    async admindata() {
      axios
        .get("http://localhost:8083/api/items5")
        .then((result) => {
          

          let alldata = result.data;
          this.CardData = result.data;
          console.log(alldata);
          for (let i = 0; i < alldata.length; i++) {
            let obj = {
              title: alldata[i].sam[1],
              partnumber: "Part No: " + alldata[i].sam[0],
              src: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRnVW06t64ntmQJ8q4zfR_wN3CQf3tWZoJTuQ&usqp=CAU",
              flex: 4,
            };
            this.cards.push(obj);
          }
          
        })
        .catch((err) => {
          
        });
      // return this.poly;
    },

    finalDate(date) {
      const month = [
        "JANUARY",
        "FEBRUARY",
        "MARCH",
        "APRIL",
        "MAY",
        "JUNE",
        "JULY",
        "AUGUST",
        "SEPTEMBER",
        "OCTOBER",
        "NOVEMBER",
        "DECEMBER",
      ];
      const weekday = [
        "SUNDAY",
        "MONDAY",
        "TUESDAY",
        "WEDNESDAY",
        "THURSDAY",
        "FRIDAY",
        "SATURDAY",
      ];
      const current = new Date();
      //D day
      let onlyday = `${current.getDate()}`;
      let tempday = "0" + onlyday;

      //DD day
      let fullday = tempday.slice(-2);
      //M
      let halfmonth = `${current.getMonth() + 1}`;

      let tempmonth = "0" + halfmonth;
      //MM
      let fullmonth = tempmonth.slice(-2);
      //January
      let letmonth = month[current.getMonth()];
      //jan
      let letmonth3 = letmonth.substring(0, 3);
      //Monday
      let letdayfull = weekday[current.getDay()];
      //Mon
      let letday = fullday.substring(0, 3);
      //YYYY
      let fullyear = `${current.getFullYear()}`;
      //Yy
      let halfyear = fullyear.slice(-2);

      if (date === "DMY1") {
        this.Date = fullday + fullmonth + fullyear;
      } else if (date === "DMY2") {
        this.Date = `${fullday}${fullmonth}${halfyear}`;
      } else if (date === "DMY3") {
        this.Date = `${onlyday}${fullmonth}${halfyear}`;
      } else if (date === "DMY4") {
        this.Date = `${onlyday}${halfmonth}${halfyear}`;
      } else if (date === "DMY5") {
        this.Date = `${onlyday}${halfmonth}${fullyear}`;
      } else if (date === "DMY6") {
        this.Date = `${onlyday}${fullmonth}${fullyear}`;
      } else if (date === "DMY7") {
        this.Date = `${fullday}${halfmonth}${fullyear}`;
      } else if (date === "DMY8") {
        this.Date = `${fullday}${halfmonth}${halfyear}`;
      } else if (date === "DMY9") {
        this.Date = `${onlyday}${halfmonth}${halfyear}`;
      }
      //3 letter
      else if (date === "DMY10") {
        this.Date = `${letday}${letmonth3}${fullyear}`;
      } else if (date === "DMY11") {
        this.Date = `${letday}${letmonth3}${halfyear}`;
      } else if (date === "DMY12") {
        this.Date = `${letday}${fullmonth}${fullyear}`;
      } else if (date === "DMY13") {
        this.Date = `${letday}${fullmonth}${halfyear}`;
      } else if (date === "DMY14") {
        this.Date = `${letday}${halfmonth}${fullyear}`;
      } else if (date === "DMY15") {
        this.Date = `${letday}${halfmonth}${halfyear}`;
      } else if (date === "DMY16") {
        this.Date = `${fullday}${letmonth3}${halfyear}`;
      } else if (date === "DMY17") {
        this.Date = `${onlyday}${letmonth3}${halfyear}`;
      } else if (date === "DMY18") {
        this.Date = `${fullday}${letmonth3}${fullyear}`;
      } else if (date === "DMY19") {
        this.Date = `${onlyday}${letmonth3}${fullyear}`;
      } else if (date === "DMY20") {
        this.Date = `${letdayfull}${letmonth}${fullyear}`;
      } else if (date === "DMY21") {
        this.Date = `${letdayfull}${letmonth}${halfyear}`;
      } else if (date === "DMY22") {
        this.Date = `${fullday}${letmonth}${halfyear}`;
      } else if (date === "DMY23") {
        this.Date = `${fullday}${letmonth}${fullyear}`;
      } else if (date === "DMY24") {
        this.Date = `${onlyday}${letmonth}${fullyear}`;
      } else if (date === "DMY25") {
        this.Date = `${onlyday}${letmonth}${halfyear}`;
      } else if (date === "DMY26") {
        this.Date = `${letdayfull}${fullmonth}${halfyear}`;
      } else if (date === "DMY27") {
        this.Date = `${letdayfull}${fullmonth}${fullyear}`;
      } else if (date === "DMY28") {
        this.Date = `${letdayfull}${halfmonth}${halfyear}`;
      } else if (date === "DMY29") {
        this.Date = `${letdayfull}${halfmonth}${fullyear}`;
      }
    },
    finalYear(year2) {
      const current = new Date();
      if (year2 === "YYYY") {
        this.year = `${current.getFullYear()}`;
      } else if (year2 === "YY") {
        const fullyear = `${current.getFullYear()}`;
        this.year = fullyear.slice(-2);
      } else if (year2 === "YYY") {
        const fullyear = `${current.getFullYear()}`;
        this.year = fullyear.slice(-2);
        this.year = Number(this.year).toString();
      }
    },
    finalDay(day2) {
      const current = new Date();
      const weekday = [
        "SUNDAY",
        "MONDAY",
        "TUESDAY",
        "WEDNESDAY",
        "THURSDAY",
        "FRIDAY",
        "SATURDAY",
      ];
      if (day2 === "DDDDD") {
        this.day = weekday[current.getDay()];
      } else if (day2 === "DDD") {
        let any = weekday[current.getDay()];
        this.day = any.substring(0, 3);
      } else if (day2 === "DDDD") {
        this.day = `${current.getDate()}`;
      } else if (day2 === "DD") {
        var temp = "";
        temp = `${current.getDate()}`;
        temp = "0" + temp;
        this.day = temp.slice(-2);
      }
    },
    finalMonth(month2) {
      const current = new Date();
      const month = [
        "JANUARY",
        "FEBRUARY",
        "MARCH",
        "APRIL",
        "MAY",
        "JUNE",
        "JULY",
        "AUGUST",
        "SEPTEMBER",
        "OCTOBER",
        "NOVEMBER",
        "DECEMBER",
      ];
      if (month2 === "MMMM") {
        this.month = month[current.getMonth()];
      } else if (month2 === "MMM") {
        let anymonth = month[current.getMonth()];
        this.month = anymonth.substring(0, 3);
      } else if (month2 === "MM") {
        var temp = "";
        temp = `${current.getMonth() + 1}`;
        temp = "0" + temp;
        this.month = temp.slice(-2);
      } else if (month2 === "M") {
        const any = current.getMonth() + 1;
        this.month = `${any}`;
      }
    },
    finalTime(time2) {
      const current = new Date();
      if (time2 === "t1") {
        this.time = `${current.getHours()}${current.getMinutes()}${current.getSeconds()}`;
      } else if (time2 === "t2") {
        this.time = `${current.getHours()}${current.getMinutes()}`;
      } else if (time2 === "t3") {
        this.time = `${current.getHours()}${current.getSeconds()}`;
      } else if (time2 === "t4") {
        this.time = `${current.getMinutes()}${current.getSeconds()}`;
      } else if (time2 === "t5") {
        this.time = `${current.getHours()}`;
      } else if (time2 === "t6") {
        this.time = `${current.getMinutes()}`;
      } else if (time2 === "t7") {
        this.time = `${current.getSeconds()}`;
      }
    },
  },
};
</script>

<style scoped>
.v-card {
  transition: opacity 0.4s ease-in-out;
}

.v-card:not(.on-hover) {
  opacity: 0.6;
}
</style>