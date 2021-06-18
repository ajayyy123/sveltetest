 <script context='module'>
export async function load({page,fetch,session,context}) {
    if(session){
        return {
           props:{
               session
           } 
        }
    }
}

</script>

<script>
export let session
import {post,browserSet} from '$lib/req_utils'
import Image from '$lib/components/image.svelte'
import Upload from '$lib/components/upload.svelte'
// import axios from "axios";
 export let data
 let file
 $:if(file){
   data1.profile=file
   data1=data1
 }
 let data1 ={
     "Name" : "testsvelte1",
     "Lastname" : "mysvelte1",
     "profile":"",
     "type" :"Fresher"
   }
  let login, signup, signout, vuser,strapi;
  let ulogin = {
    "auth": "login",
 	"c_id": "3v9h9sli9f0c4bhepe81vsho1j",
	"pool_id":"p-south-1_9WoXGfjYO",
    "user": "",
    "pass": ""
  };
  let usignup = {
    usrname: "",
    password: ""
  };
  let uvuser = {
    usrname: "",
    password: ""
  };
 async function handlestrapi(){
     const json=await post(fetch,'http://localhost:1337/auth/local',{
         identifier:ulogin.username,
         password:ulogin.password
     });
     console.log(json);
     if (json.jwt){
        //  console.log(res.body.jwt)
        browserSet('jwt',json.jwt)

     }
 }
	async function msignout(){
         console.log("check",document.cookie)
        console.log('Signout clicked')
// const invocation = new XMLHttpRequest();
// const url = 'http://localhost:4500/users/signout';
// if (invocation) {
//     invocation.open('GET', url, true);
//     invocation.withCredentials = true;
//     // invocation.onreadystatechange = handler;
//     invocation.send();
//   }

        // try {
        //     const fetchData = await axios({
        //       url: 'http://localhost:4500/users/signout',
        //       method: 'get',
        //       mode:"cors",

        //     //   withCredentials: true,
        //       headers: {
        //            'Content-Type' : 'application/x-www-form-urlencoded; charset=UTF-8',
        //           withCredentials: true
        //         // 'x-api-key': 'da2-p2rxa6aypjfgfjhzwodpexipyu'
        //       },
        //     //   data: {
        //     //     query: print(eval(req.body.oper)),
        //     //   }
        //     });
        //     // const body = {
        //     //     graphqlData: graphqlData.data.data.eval(req.body.oper)
        //     // }
        //     console.log(JSON.stringify(fetchData.text()))
            // res.status(200).json(body.graphqlData.items)
            // return {
            //     statusCode: 200,
            //     body: JSON.stringify(body),
            //     headers: {
            //         "Access-Control-Allow-Origin": "*",
            //     }
            // }
        //   } catch (err) {
        //     console.log('error posting to appsync: ', err);
        //   } 
         data={
      "auth": "login",
    }
 const res = await fetch(
   
        "https://9zmpmxira4.execute-api.ap-south-1.amazonaws.com/default/botocognitoauth",
        {
          method: "POST",
          mode: "cors",
         
            //  credentials:'include',
          // credentials: "same-origin",
             headers: { "Content-Type": "application/json",'x-api-key':"OPmz5AOHfP4jjxGfANMhmbICUjdX19d3WQT4HY41"},
        // headers: { "Content-Type": "application/json", "Access-Control-Allow-Credentials": true },
           body: JSON.stringify(data)
    
        }
      );
     res.text().then((e) =>{

			 console.log(e)})
	}
	
  async function cuser(){
    //    console.log("check",document.cookie)
   const res = await fetch(
        "http://localhost:4500/users/currentuser",
        {
          method: "GET",
          mode: "cors",
          headers: { "Content-Type": "application/json" },
              
        }
      );
     res.text().then((e) =>{

			 console.log(e)})
		
       
	}
	
    async function sulogin() {
      // 		data=data
      const res = await fetch(
        "https://9zmpmxira4.execute-api.ap-south-1.amazonaws.com/default/botocognitoauth",
        {
          method: "POST",
          mode:"cors",
          // mode: "same-origin",
          // credentials:'same-origin',
           headers: { "Content-Type": "application/json",'x-api-key':'OPmz5AOHfP4jjxGfANMhmbICUjdX19d3WQT4HY41' },
          // headers: { "Content-Type": "application/json","Access-Control-Allow-Credentials": true},
          body: JSON.stringify(ulogin)
        }
      );
     res.json().then((e) =>{

			 console.log(e)})
		
       
       
    }
   
  function mlogin() {
    login = true;
    signup = false;
    signout = false;
    vuser = false;
  }

  function msignup() {
    login = false;
    signup = true;
    signout = false;
    vuser = false;
  }
//   function msignout() {
//     login = false;
//     signup = false;
//     signout = true;
//     vuser = false;
//   }
  function mvuser() {
    login = false;
    signup = false;
    signout = false;
    vuser = true;
  }
  function setstrapi(){
      strapi=true;
  }
  async function checkstrapi(){
   
  
   const res = await fetch(
        "http://localhost:1337/upload",
        {
          method: "POST",
          // mode: "cors",
          
          headers: { "Content-Type": "application/json", },
          body: JSON.stringify(file)
        }
      );
     res.json().then((e) =>{

			 console.log(e)})
		
       
  }
</script>

<div>
  <button on:click={mlogin}>Login</button>
  <button on:click={msignup}>Signup</button>
  <button on:click={msignout}>Signout</button>
  <button on:click={mvuser}>Verifyuser</button>
	<button on:click={cuser}>Currentuser</button>
	<button on:click={setstrapi}>strapi</button>
</div>
{#if login}
  user:
  <input type="text" bind:value={ulogin.user} />
  passwd:
  <input type="password" bind:value={ulogin.pass} />
  <button on:click={sulogin} >Submit</button>
{/if}
{#if strapi}
  user:
  <input type="text" bind:value={ulogin.username} />
  passwd:
  <input type="password" bind:value={ulogin.password} />
  <button on:click={handlestrapi} >Submit</button>
{/if}
{JSON.stringify(ulogin)}
{data}

<div>
<Image bind:file={file}>
  
{#if file}
<button on:click={checkstrapi}>Submitfile</button>
{/if}
 
</Image>
<slot></slot>
{file}
<Upload></Upload>
</div>

{"session"}:{JSON.stringify(session)}