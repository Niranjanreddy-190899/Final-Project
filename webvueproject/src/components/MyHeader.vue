<template>


    <h2> {{ WebsiteName }}</h2>
    <h2> {{ authorName }}</h2>
  </template>
  
  <script>
  
  
   
  
  export default {
    name: 'MyHeader',
    props: {
        WebsiteName: String,
        authorName: String
    }
    
  }
  
  
  
  
  </script>
  
  
  <style>
  
  
  </style>