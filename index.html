// Install required dependencies: express, axios, dotenv
// npm install express axios dotenv

const express = require('express');
const axios = require('axios');
const path = require('path');
require('dotenv').config();

const app = express();
const PORT = 3000;

// Middleware for parsing JSON
app.use(express.json());

// Serve static files (HTML, CSS, JS)
app.use(express.static(path.join(__dirname, 'public')));

// Facebook App credentials
const FB_APP_ID = process.env.FB_APP_ID;
const FB_APP_SECRET = process.env.FB_APP_SECRET;
const REDIRECT_URI = `http://localhost:${PORT}/fb-callback`;

// Route: Home page
app.get('/', (req, res) => {
  res.sendFile(path.join(__dirname, 'public', 'index.html'));
});

// Route: Facebook Login Redirect
app.get('/login-facebook', (req, res) => {
  const fbLoginURL = `https://www.facebook.com/v12.0/dialog/oauth?client_id=${FB_APP_ID}&redirect_uri=${REDIRECT_URI}&scope=email,public_profile`;
  res.redirect(fbLoginURL);
});

// Route: Facebook OAuth Callback
app.get('/fb-callback', async (req, res) => {
  const { code } = req.query;
  if (!code) return res.status(400).send('Authorization code is missing.');

  try {
    // Exchange code for access token
    const tokenResponse = await axios.get(
      `https://graph.facebook.com/v12.0/oauth/access_token`,
      {
        params: {
          client_id: FB_APP_ID,
          redirect_uri: REDIRECT_URI,
          client_secret: FB_APP_SECRET,
          code,
        },
      }
    );

    const accessToken = tokenResponse.data.access_token;

    // Fetch user data
    const userResponse = await axios.get('https://graph.facebook.com/me', {
      params: {
        fields: 'id,name,email',
        access_token: accessToken,
      },
    });

    const userData = userResponse.data;

    res.send(`
      <h1>Welcome, ${userData.name}</h1>
      <p>Email: ${userData.email}</p>
      <form action="/delete-data" method="POST">
        <input type="hidden" name="access_token" value="${accessToken}" />
        <button type="submit">Delete My Email/Phone</button>
      </form>
    `);
  } catch (error) {
    console.error(error);
    res.status(500).send('Error during Facebook OAuth process.');
  }
});

// Route: Delete Data (Mock)
app.post('/delete-data', async (req, res) => {
  const { access_token } = req.body;

  try {
    // Request user data deletion through Facebook API
    await axios.delete(`https://graph.facebook.com/me/permissions`, {
      params: { access_token },
    });

    res.send('<h1>Your data has been deleted from this application.</h1>');
  } catch (error) {
    console.error(error);
    res.status(500).send('<h1>Failed to delete data. Please try again later.</h1>');
  }
});

// Route: User Data Deletion Callback (Facebook requirement)
app.post('/facebook-data-deletion', (req, res) => {
  const { signed_request } = req.body;

  if (!signed_request) {
    return res.status(400).send('Invalid request');
  }

  // Decode signed_request
  const [encodedSig, payload] = signed_request.split('.');
  const data = JSON.parse(Buffer.from(payload, 'base64').toString('utf-8'));

  if (data.user_id) {
    // Respond with deletion confirmation
    return res.json({ url: `http://localhost:${PORT}/data-deletion-confirmation`, confirmation_code: data.user_id });
  }

  res.status(400).send('User ID not found in request');
});

// Route: Data Deletion Confirmation Page
app.get('/data-deletion-confirmation', (req, res) => {
  res.send('<h1>Your data deletion request has been received and is being processed.</h1>');
});

// Start server
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
