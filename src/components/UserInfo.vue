<template>
    <div class="card" >
        <div class="image">
            <img :src="userInfo.image" alt="Avatar">
        </div>
        <div class="data">
            <h2>{{userInfo.name}}</h2>
            <p class="username">@{{userInfo.user_name}}</p>
            <p class="join-date">Joined {{standardDateAndTime(userInfo.joined)}}</p>
            <p class="bio" v-if="userInfo.bio !== null ">{{userInfo.bio}}</p>
            <p class="bio" v-else>This profile has no bio...</p>
            <div class="follower-info">
                <div class="repos">
                    <span class="stats-headings">Repos</span>
                    <br/>
                    <span class="stats">{{userInfo.repos}}</span>
                </div>
                <div class="followers">
                    <span class="stats-headings">Followers</span>
                    <br/>
                    <span class="stats">{{userInfo.followers}}</span>
                </div>
                <div class="following">
                    <span class="stats-headings">Following</span>
                    <br/>
                    <span class="stats">{{userInfo.following}}</span>
                </div>
            </div>

            <div class="links">
                <div class="twitter-and-location">
                    <div>
                        <img src="../assets/location-icon.svg" alt="location" class="social-icon">
                        <span class="social-links" v-if="userInfo.location !== null ">{{userInfo.location}}</span>
                        <span class="social-links" v-else>Not available</span>
                    </div>
                    <div class="twitter-links">
                        <img src="../assets/twitter-icon.svg" alt="twitter" class="social-icon">
                        <span class="social-links" v-if="userInfo.twitter !== null">{{userInfo.twitter}}</span>
                        <span class="social-links" v-else>Not available</span>
                    </div>
                </div>
         </div>

            <div class="website-and-company">
                <div>
                    <img src="../assets/website-icon.svg" alt="website" class="social-icon">
                    <span class="social-links" v-if="userInfo.blog !== ''">{{userInfo.blog}}</span>
                    <span class="social-links" v-else>Not available</span>
                </div>
                <div>
                    <img src="../assets/company-icon.svg" alt="company" class="social-icon">
                    <span class="social-links" v-if="userInfo.company !== null">{{userInfo.company}}</span>
                     <span class="social-links" v-else>Not available</span>
                </div>
            </div>
        </div>
    </div>
</template> 



<script>

import moment from 'moment'
export default {
    props: ['userInfo'],

    setup() {
        const standardDateAndTime = (value) => {
             return moment(value).format("DD-MM-YYYY")
        } 

        return {
            standardDateAndTime
        }
    }
}

</script> 

