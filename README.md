# Spotify Now Playing [![Deploy to Vercel](https://vercel.com/button)](https://vercel.com/import/project?template=https://github.com/joshlmao/now-playing-profile)

<a href="https://now-playing-profile.rajitbanerjee.vercel.app/now-playing?open">
    <img src="https://now-playing-profile.rajitbanerjee.vercel.app/now-playing" width="256" height="64" alt="Now Playing">
</a>

### Part 1: Vercel Deployment

1. Sign-up/sign-in to use [Vercel](https://vercel.com/) for hosting the repo.
2. Fork [natemoo-re's original repo](https://github.com/natemoo-re/natemoo-re), or [joshlmao's now-playing-profile repo](https://github.com/JoshLmao/now-playing-profile) which is just a skeleton repo that contains the Spotify Now Playing specific features.
3. Go to your Vercel dashboard and select **Import a Git Repository**.
4. Paste the Git URL of your forked repo. For example, "https://github.com/JoshLmao/now-playing-profile".

   <img src="https://i.imgur.com/fkiH4QL.png" height="250">

5. Leave the remaining settings for now and click **Deploy**.

### Part 2: Configure Environment Variables

1. Create a new app from your [Spotify Dashboard](https://developer.spotify.com/dashboard/).

   <img src="https://i.imgur.com/msl76HF.png" height="300">

2. Click **Edit Settings** and add "https://localhost:3000/callback" to the **Redirect URIs** section.

   <img src="https://i.imgur.com/wm4IoDH.png" height="400">

3. Next, we need to do a [Authoration Code flow](https://developer.spotify.com/documentation/general/guides/authorization-guide/#authorization-code-flow) auth request to retrieve a Refresh Token.

   - Replace "MY_CLIENT_ID" in the following URL with your Client ID from your Spotify Dashboard and paste the URL in your browser. Your Client ID and Secret ID can be found in your Spotify dashboard (as shown below).

   https://accounts.spotify.com/authorize?client_id=MY_CLIENT_ID&response_type=code&redirect_uri=https%3A%2F%2Flocalhost%3A3000%2Fcallback&scope=user-read-playback-state%20user-read-currently-playing
   
   <img src="https://i.imgur.com/VzY5Uxv.png" >

   - Once done, you will get a blank page with a different URL which is like "https://localhost:3000/callback?code=MY_CODE".

   - Next, navigate to [Base64Encode](https://www.base64encode.org/) and insert your Client ID and Secret ID **separated by a colon**. For example, "CLIENT_ID:SECRET_ID".

   - Then, insert **MY_BASE_64_STRING** and **MY_CODE** from the previous steps in the following command and press enter to run.

   ```bash
   curl -H "Authorization: Basic MY_BASE_64_STRING" \
   -d grant_type=authorization_code \
   -d code=MY_CODE \
   -d redirect_uri=https%3A%2F%2Flocalhost%3A3000%2Fcallback https://accounts.spotify.com/api/token
   ```
   
   <img src="https://i.imgur.com/tnaCoqj.png">

   - Once done correctly, you will get JSON which contains your refresh token, shown in the blue box in the image above. Take out the refresh token, blocked out in green above, and save it somewhere

4. Navigate to your deployment on Vercel, and go to **Settings** > **Environment Variables**.

   <img src="https://i.imgur.com/kUEW5Tt.png" height=400 />

5. For each of these variable names and insert your values from the previous steps.

```
Name: SPOTIFY_CLIENT_ID
Value: MY_CLIENT_ID

Name: CLIENT_SECRET
Value: MY_SECRET_ID

Name: SPOTIFY_REFRESH_TOKEN
Value: MY_REFRESH_TOKEN
```

6. Once done, navigate to one of your deployment URL's (_note_: a new deployment is required, which is triggered by any push to the master branch of your repository linked to Vercel) and place "/now-playing" at the end. For example, "https://now-playing-joshlmao.vercel.app/now-playing"

7. Replace "MY_VERCEL_DEPLOYMENT_URL" in the following code with one of your deployment URL's and insert it into any Markdown/HTML file (e.g. your GitHub profile README)

```
<a href="https://MY_VERCEL_DEPLOYMENT_URL/now-playing?open">
    <img src="https://MY_VERCEL_DEPLOYMENT_URL/now-playing" width="256" height="64" alt="Now Playing">`
</a>
```

That's it! Below is an example of what it should look like. If you have any problems, make sure to re-read the instructions and follow them precisely!

<img src="https://i.imgur.com/uxeiC8k.png">
