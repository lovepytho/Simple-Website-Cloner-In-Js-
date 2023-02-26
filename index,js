const fetch = require('node-fetch');
const fs = require('fs');
const path = require('path');

const url = 'https://vanikacodez.tech';

fetch(url)
  .then(response => {
    if (!response.ok) {
      throw new Error(`error http ka: ${response.status}`);
    }
    return response.text();
  })
  .then(data => {
    
    fs.writeFile('idk.html', data, (err) => {
      if (err) {
        console.log(`error agaya: ${err.message}`);
      } else {
        console.log('cloned html');
      }
    });

   
    const cssRegex = /href="(.*?\.css)"/gm;
    const match = cssRegex.exec(data);
    if (match && match[1]) {
      const cssUrl = new URL(match[1], url);
      // Fetch CSS file
      fetch(cssUrl)
        .then(response => {
          if (!response.ok) {
            throw new Error(`error : ${response.status}`);
          }
          return response.text();
        })
        .then(cssData => {
         
          fs.writeFile('styles.css', cssData, (err) => {
            if (err) {
              console.log(`error: ${err.message}`);
            } else {
              console.log('cloned css');
            }
          });
        })
        .catch(error => {
          console.log(`Error fetching CSS file: ${error.message}`);
        });
    } else {
      console.log('No CSS file found');
    }
  })
  .catch(error => {
    console.log(`website he bhi?: ${error.message}`);
  });
