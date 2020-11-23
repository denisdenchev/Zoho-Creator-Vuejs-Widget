<template>
<div id="container">
  <div v-bind:class="[submitFormActive ? 'submitFormContainer' : 'hide']">
    <h1>Register new employee</h1>
    <div id="submitForm">
      <div id="personalInformation">
        <field field_label ='First Name *'  v-model="fname"></field>
        <field field_label ='Last Name *' v-model="lname"></field>
        <field field_label ='Date of Birth *' placeholder="Example: 10/05/2005" v-model="dob"></field>
        <emailfield field_label='Email *' v-model="email" placeholder="example@gmail.com"></emailfield>
        <mobilefield field_label ='Mobile *' v-model="mobile"></mobilefield>
        <mobilefield field_label ='Next Of Kin Mobile *' v-model="nextOfKinMobile"></mobilefield>
        <field field_label ='URL of a Profile Image' v-model="profileImageUrl"></field>
      </div>
      <div id="addressInformation">
        <field field_label ='Address Line 1 *' v-model="addressLineOne"></field>
        <field field_label ='Address Line 2' v-model="addressLineTwo"></field>
        <field field_label ='City *' v-model="city"></field>
        <field field_label ='County *' v-model="county"></field>
        <field field_label ='Post Code *' v-model="postCode"></field>
        <field field_label ='Country *' v-model="country"></field>
        <field field_label ='Job Title *' v-model="jobTitle"></field>
      </div>
    </div>
    <div id="buttonComponent">
    <submitbutton button_label="Submit" @click="createRecord()"></submitbutton>
    </div>
  </div>
  <div class="employeesButtons">
    <submitbutton button_label="See employees" @click="fetchRecords()"></submitbutton>
    <!-- <submitbutton button_label="See projects" @click="fetchProjectRecords()"></submitbutton> -->
    <div v-bind:class="[isButtonActive ? 'show' : 'hide']">
      <submitbutton button_label="Add Employee" @click="toggleClassSubmitForm()"></submitbutton>
    </div>
  </div>
  <div class="employeesContainer" >
    <div v-bind:class="[showEmployees ? 'employeeContainer' : 'hide']" v-for="rec in listOfEmployees" v-bind:key="rec.ID"  >
      <div class="wrapper" v-if="rec.id !== null">
        <div class="card">
          <div class="front">
            <h2>{{rec.name.display_value}}</h2>
            <img :src="rec.image_url" alt="image of person">
            <h2>{{rec.job_title}}</h2>
            <!-- <p v-for="rec in response.data" :key="email"></p> -->
          </div>
          <div class="right">
            <ul>
              <li>Date Of Birth: <span>{{rec.date_of_birth}}</span></li>
              <li>Email: <span>{{rec.email}}</span></li>
              <li>Mobile: <span>{{rec.phone_number}}</span></li>
              <li>Next Of Kin Mobile: <span>{{rec.next_of_kin_phone_number}}</span></li>
              <li>Address Line 1: <span>{{rec.address.address_line_1}}</span></li>
              <li>Address Line 2: <span>{{rec.address.address_line_2}}</span></li>
              <li>City: <span>{{rec.address.district_city}}</span></li>
              <li>County: <span>{{rec.address.state_province}}</span></li>
              <li>Post Code: <span>{{rec.address.postal_code}}</span></li>
              <li>Country: <span>{{rec.address.country}}</span></li>
            </ul>
            <!-- This is the button that triggers the action for all of them -->
            <button class="projectsWorkingOnButton" @click="toggleClass(rec.ID)">Projects Working On</button>
          </div>
        </div>
          <div v-bind:class="[rec.visible ? 'projectsWorkingOnActive' : 'projectsWorkingOnInactive']" v-for="proj in dummyProjectsData" v-bind:key="proj.id" >
            <div v-if="rec.name.display_value == proj.task_owner">
              <h3>Projects Working On</h3>
              <ul>
                <li v-for="p in proj.projects_working_on" v-bind:key="p.project_id">
                  <a href="">{{ p.project_name }}</a>
                </li>
                <li><submitbutton button_label="Hide Projects" @click="toggleClass(rec.ID)"></submitbutton></li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
module.exports = {
  name: 'submit',
  props: {
  },
  components: {
    'field': httpVueLoader('./field.vue'),
    'emailfield': httpVueLoader('./emailfield.vue'),
    'mobilefield': httpVueLoader('./mobilefield.vue'),
    'submitbutton': httpVueLoader('./submitbutton.vue'),
  },
  data: () => {
    return {
      fname: '',
      lname: '',
      dob: '',
      email: '',
      addressLineOne: '',
      addressLineTwo: '',
      city: '',
      county: '',
      postCode: '',
      country: '',
      mobile: '',
      nextOfKinMobile: '',
      profileImageUrl: '',
      jobTitle: '',
      isActive: false,
      isButtonActive: true,
      submitFormActive: false,
      listOfEmployees: undefined,
      listOfProjectOwners: undefined,
      showEmployees: false,
      dummyProjectsData: [
        {
          ID: "44000005501077",
          task_owner: "Denis Denchev",
          visible: false,
          projects_working_on: [
            {
            "project_name": "Denis Denchev - Project-1",
            "project_id": "195000002362044",
            },
            {
            "project_name": "DD - Project-5",
            "project_id": "195000002362045"
            },
            {
            "project_name": "DD - Project-3",
            "project_id": "195000002362046"
            },
          ]
        },
        {
          ID: "44000005501078",
          task_owner: "Jake Jones",
          visible: false,
          projects_working_on: [
            {
            "project_name": "Jake-Jones - Project-2",
            "project_id": "195000002362044"
            },
            {
            "project_name": "JJ - Project-5",
            "project_id": "195000002362045"
            },
            {
            "project_name": "JJ - Project-3",
            "project_id": "195000002362046"
            },
          ]
        },
        {
          ID: "44000005501078",
          task_owner: "Elena Gente",
          visible: false,
          projects_working_on: [
            {
            "project_name": "Velvet 915",
            "project_id": "195000002362044"
            },
            {
            "project_name": "Elena Project",
            "project_id": "195000002362045"
            },
            {
            "project_name": "Hairstyle",
            "project_id": "195000002362046"
            },
          ]
        },
      ]
    }
  },
  methods: {
    resetFormField: function(){
      this.fname = '';
      this.lname = '';
      this.dob = '';
      this.email = '';
      this.addressLineOne = '';
      this.addressLineTwo = '';
      this.city = '';
      this.county = '';
      this.postCode = '';
      this.country = '';
      this.mobile = '';
      this.nextOfKinMobile = '';
      this.profileImageUrl = '';
      this.jobTitle = '';
    },
    toggleEmployeesDisplay: function(){
      this.showEmployees = !this.showEmployees
    },
    toggleButtonActive: function(){
      this.isButtonActive = !this.isButtonActive
    },
    toggleClassSubmitForm: function(event){
      this.submitFormActive = !this.submitFormActive;
      var ref1 = this;
      ref1.resetFormField();
      this.showEmployees = false;
    },
    toggleClass: function(id){
      i = -1
      for (let index = 0; index < this.listOfEmployees.length; index++) {
        const employee = this.listOfEmployees[index];
        i = employee.ID == id ? index : i
      }
      var rec1 = this.listOfEmployees[i]
      rec1.visible = !rec1.visible
      this.listOfEmployees.splice(i,1,rec1)
    },
    fetchRecords() {
      ZOHO.CREATOR.init().then((data) => {
        var config = {
						reportName: 'Register_Form_Report',
          };
          ZOHO.CREATOR.API.getAllRecords(config).then((response) => {
            this.listOfEmployees = response.data
            console.log(this.listOfEmployees);
          })
          ref2 = this;
          ref2.toggleEmployeesDisplay();
          // this.fetchProjectRecords();
      })
    },
    // fetchProjectRecords() {
    //   ZOHO.CREATOR.init().then((data) => {
    //     var config = {
		// 				reportName: 'Tasks_Report',
    //       };
    //       ZOHO.CREATOR.API.getAllRecords(config).then((response) => {
    //         const records = response.data;
    //         var names = [];
    //         records.forEach(rec => {
    //           names.push(rec.task_owner)
    //         });
    //         const namesArray = new Set(names);
    //         const namesArrayNoDupes = [...namesArray];
    //         this.listOfProjectOwners = namesArrayNoDupes;
    //         console.log(this.listOfProjectOwners);
    //       })
    //   })
    // },
    createRecord() {
      var ref=this;
      ZOHO.CREATOR.init().then((data) => {
        form_submission_data = {
          data: {
            name: {
              first_name: this.fname,
              last_name: this.lname,
            },
            address: {
              address_line_1: this.addressLineOne,
              address_line_2: this.addressLineTwo,
              country: this.country,
              // display_value: 'display value of address',
              district_city: this.city,
              postal_code: this.postCode,
              state_province: this.county,
            },
            email: this.email,
            phone_number: this.mobile,
            next_of_kin_phone_number: this.nextOfKinMobile,
            job_title: this.jobTitle,
            // image: `${profileImg}`,
            image_url: this.profileImageUrl,
            date_of_birth: this.dob,
          },
        };

        var data = {
          formName: 'Register_Form',
          data: form_submission_data,
        };

        ZOHO.CREATOR.API.addRecord(data)
          .then(function (response) {
            if (response.code == 3000) {
              console.log('Record added successfully');
              alert('Form has been successfully submitted');
              ref.toggleClassSubmitForm();
              // ref.toggleButtonActive();
            } 
          })
          .catch((err) => console.log(err));
      });
    },
  }
}
</script>



<style scoped>
/* Styling for card */


@import url('https://fonts.googleapis.com/css?family=Sarala:700|Exo+2:300');

*,
*:before,
*:after{
  box-sizing: border-box;
  -webkit-tap-highlight-color: rgba(255,255,255,0);
  outline: 1px solid transparent;
}

body{ 
  display: flex;
  width: 100vw;
  height: 100vh;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin: 0;
  padding: 0;
  overflow: hidden;
  background-image: linear-gradient(-55deg, rgba(50,45,55,1) 0%, rgba(101,96,106,1) 100%);
  color: #f5f5f5;
  font-family: 'Exo 2';
  font-weight: 300;
  animation: fadeIn .5s cubic-bezier(0.390, 0.575, 0.565, 1.000) 1;
}

.wrapper{
  width: 280px;
  height: 480px;
  perspective: 800px;
  position: relative;
  margin: 30px 0;
}

.card{
  width: 320px;
  height: 450px;
  position: relative;
  transform-style: preserve-3d;
  transform: translateZ(-140px);
  transition: transform 350ms cubic-bezier(0.390, 0.575, 0.565, 1.000);
  cursor: pointer;
}

.card > div{
  position: absolute;
  width: 320px;
  height: 450px;
  padding: 5px 21px;
  transition: all 350ms cubic-bezier(0.390, 0.575, 0.565, 1.000);
}

.front{
  background-image: linear-gradient(180deg, blueviolet 0%, rgba(0, 26, 82, 0.87) 100%);
  transform: rotateY(0deg) translateZ(160px); 
  border-radius: 34px 3px 0 0;
  overflow: hidden;
}



.front img {
  object-fit: cover;
  object-position: center;
  width: 100%;
  height: 75%;
  border-radius: 10px;
}

.front h2 {
  color: white;
  margin: 10px 0;
  text-align: center;
}

.right{ 
  background-image: linear-gradient(0deg, rgb(0, 192, 48) 0%, blueviolet 100%);
  opacity: 0.08;
  transform: rotateY(90deg) translateZ(160px);
  border-radius: 0 0 3px 34px;
}

.projectsWorkingOnActive {
  padding: 20px 0;
}

.projectsWorkingOnActive h3 {
  color: pink;
}

.projectsWorkingOnInactive {
  display: none;
}

.projectsWorkingOnActive h3 {
  text-align: center;
  margin: 10px 0;
}

.projectsWorkingOnActive ul li {
  margin: 10px 0;
  text-align: center;
}


.projectsWorkingOnActive ul li a{
  text-decoration: none;
  color: black;
  font-size: 18px;
  font-weight: 600;
}

.projectsWorkingOnActive ul li a:hover{
  color: blue;
}

.employeesButtons {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
  margin: 20px 0;
}



.card:hover{
  transform: translateZ(-160px) rotateY( -90deg);
}

.card:hover .front{
  opacity: 0; 
}

.card:hover .right{
  opacity: 1; 
}


@keyframes float{
  0%{
    transform: translateZ(20px);
  }
  100%{
    transform: translateY(-21px) translateX(-13px) translateZ(30px);
  }
}

/* .card:hover ~ .img-wrapper img{
  transform: scale(0.9) translateX(77%) translateY(90%) rotateZ(80deg);
} */

.right ul{
  padding: 20px 0;
}

.right ul li{
  list-style: none;
  padding-bottom: 8px;
  position: relative;
  color: black;
  font-weight: 500;
  font-size: 17px;
}

.right ul li span {
  font-weight: 700;
  color: white;
}



.projectsWorkingOnButton{
  position: absolute;
  right: 21px; 
  bottom: 34px;
  border: none;
  box-shadow: none;
  background: none;
  color: white;
  font-family: 'Exo 2';
  font-weight: 700;
  font-size: 15px;  
  letter-spacing: -.25px;
  font-weight: 700;
  padding: 13px 34px;
  border-radius: 55px 55px 21px 55px;
  background-image: linear-gradient(130deg, rgba(117,51,165,1)  50%, rgba(51,46,57,.89) 100%);
  background-size: 125% 100%;
  background-position: right;
  cursor: pointer;
  box-shadow: 8px 5px 13px rgba(34,34,34,.08);
  transform: scale(0) skewY(13deg);
  transition: all 150ms cubic-bezier(0.390, 0.575, 0.565, 1.000);
  transform-origin: right bottom;
}

.card:hover .projectsWorkingOnButton{
  transform: scale(1) skewY(0);
}

.card:not(:hover) .projectsWorkingOnButton{
opacity: 0;
}

.projectsWorkingOnButton:hover{
  background-position: left;
}


@keyframes fadeIn{
  0%{
    opacity: 0.33;
    transform: scale(.89);
  }
}

@media only screen and (max-width: 600px){
  body{
    transform: scale(.67);
  }
}




/*  */
#buttonComponent {
  display: flex;
  flex-direction: row;
  justify-content: center;
  margin: 20px 0;
}

.submitFormContainer {
  background-color: blueviolet;
  padding: 20px 0;
}

.hide {
  display: none;
}

.display {
  display: inline-block;
}

.employeesContainer {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}

.submitFormContainer h1 {
  text-align: center;
  color: white;
  text-shadow: 0px 5px 10px black ;
}

#submitForm {
  display: flex;
  flex-direction: row;
  justify-content: space-evenly;
}

#personalInformation {
  width: 35%;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}

#addressInformation {
  width: 35%;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
}
</style>



