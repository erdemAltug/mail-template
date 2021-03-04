<template>
  <center>
    <div>
      <table>
        <tr>
          <td>
            <table class="logo" width="100%" style="border-spacing: 0">
              <tr>
                <td
                  style="
                    background-color: #f6f9fc;
                    padding: 10px;
                    text-align: center;
                  "
                >
                  <a href="https://www.pixselect.com.tr">
                    <img
                      src="https://www.pixselect.com.tr/images/logos/logo.png"
                      width="180"
                      alt="Logo"
                      title="Logo"
                  /></a>
                </td>
              </tr>
            </table>
          </td>
        </tr>

        <!--  Image upload will be included next versions.

      <tr>
        <td>
          <table width="100%" style="border-spacing: 0;">
            <tr>
              <td style="padding: 10px;" >
                <label>File
        <input type="file" id="file" ref="file" v-on:change="handleFileUpload()"/>
                </label>
              </td>
            </tr>
          </table>
        </td>
      </tr>

       -->

        <tr>
          <td>
            <table>
              <tr>
                <td>
                  <label class="p-1" for="mail">
                    <strong>To whom : </strong>
                  </label>

                  <input
                    type="email "
                    class="mail"
                    v-model="mail"
                    placeholder="user@example.com"
                    size="65"
                  />
                </td>
              </tr>
            </table>
          </td>
        </tr>
        <br />

        <tr>
          <td>
            <table>
              <tr>
                <td>
                  <label class="p-1" for="Customer">
                    <strong>Customer: </strong>
                  </label>
                  <input
                    type="text "
                    class="customer"
                    v-model="customer"
                    placeholder="Dear example"
                    size="65"
                  />
                </td>
              </tr>
            </table>
          </td>
        </tr>
        <br />

        <tr>
          <td>
            <table>
              <tr>
                <td>
                  <label class="p-1" for="firstTitle">
                    <strong>First Title: </strong>
                  </label>
                  <input
                    type="text "
                    class="firstTitle"
                    v-model="firstTitle"
                    placeholder="General Title"
                    size="65"
                  />
                </td>
              </tr>
            </table>
          </td>
        </tr>
        <br />

        <tr>
          <td>
            <table>
              <tr>
                <td>
                  <label class="p-1" for="versionExplanation">
                    <strong> Customer Message : </strong>
                  </label>
                  <br />
                  <textarea
                    class="versionExplanation"
                    v-model="versionExplanation"
                    placeholder="Customer Explanation "
                    rows="10"
                    cols="80"
                  ></textarea>
                </td>
              </tr>
            </table>
          </td>
        </tr>
        <br />

        <tr>
          <td>
            <table>
              <tr>
                <td>
                  <label class="p-1" for="version">
                    <strong>Version T: </strong>
                  </label>
                  <input
                    type="text "
                    class="firstTitle"
                    v-model="version"
                    placeholder="Version Title"
                    size="65"
                  />
                </td>
              </tr>
            </table>
          </td>
        </tr>
        <br />

        <tr>
          <td>
            <table>
              <tr>
                <td>
                  <label class="p-1" for="content ">
                    <strong> Version Content : </strong>
                  </label>
                  <br />
                  <textarea
                    class="content"
                    v-model="content"
                    placeholder="Version Info"
                    rows="10"
                    cols="80"
                  ></textarea>
                </td>
              </tr>
            </table>
          </td>
        </tr>
        <br />
        <button
          id="button"
          type="button"
          class="btn btn-success btn-lg"
          v-on:click="saveMail()"
        >
          Save
        </button>
      </table>
    </div>
  </center>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      url: process.env.VUE_APP_API_ENDPOINT || '/',
      mail: "",
      customer: "",
      versionExplanation: [],
      content: [],
      firstTitle: "",
      version: "",
    };
  },

  methods: {
    /*File upload function 
     handleFileUpload(){
        this.file = this.$refs.file.files[0];
      }, */

    /* 
      axios.post(this.url, {
         content: this.content,
        })
          .then((response) => {
            console.log(response);
          }, (error) => {
            console.log(error);
          });
          
        */

    /* saveContent(){
         let textarea = document.querySelector('content');
         let textareaValue = textarea.value;
         this.content = textareaValue.split('\n');
       }, */

    saveMail() {
      console.log("email: ", this.mail);
      console.log("content: ", this.content.split("\n"));
      console.log("Customer", this.customer);
      console.log("Customer Message : ", this.versionExplanation.split("\n"));
      console.log("first title: ", this.firstTitle);
      console.log("version title", this.version);
      axios
        .post(`${this.url}/sendMail`, {
          mail: this.mail,
          content: this.content.split("\n"),
          versionExplanation: this.versionExplanation.split("\n"),
          firstTitle: this.firstTitle,
          customer: this.customer,
          version: this.version,
        })
        .then((response) => (this.responseData = response.data))
        .catch((error) => {
          this.errorMessage = error.message;
          console.error("There was a error", error);
        });
    },
  },

  /* watch:{
      content(){
        this.$emit('input' , this.content)
      }
    } */
};
</script>

<style type="text/css">
.versionExplanation {
  text-transform: capitalize;
}
.customer {
  content: "Dear Example";
  padding-bottom: 5px;
  margin-bottom: 5px;
}
.title {
  content: "Title";
  padding-bottom: 5px;
  margin-bottom: 5px;
}

.mail {
  content: "To Who";
  padding-bottom: 5px;
  margin-bottom: 5px;
}

.logo {
  margin: 5px;
  padding-bottom: 5px;
}

#button {
  width: 20%;
  float: right;
}

.content {
  text-transform: capitalize;
  width: 100%;
}

.outer {
  margin: 0 auto;
  width: 100%;
  max-width: 600px;
  border-spacing: 0;
  font-family: sans-serif;
  color: #4a4a4a;
}

template {
  margin: 0;
  padding: 0;
  background-color: #f6f9fc;
}

table {
  border-spacing: 0;
}

td {
  padding: 0;
}

img {
  border: 0;
}

@media screen and (max-width: 600px) {
}

@media screen and (max-width: 400px) {
}
</style>
