<template>
    <div class="post" v-for="post in posts" :key="post.id">
        <a target="_blank" :href="(post.user.links.html+'/?client_id='+token)" class="user">
            <div class="user__profile_photo" v-if="post.user.profile_image">
                <img :src="post.user.profile_image.medium" alt="profile photo">
            </div>
            <div class="user__profile_photo" v-else>
                <img src="@/assets/images/profile-photo.png" alt="profile photo">
            </div>
            <div class="user__info">
                <p class="user__name">{{ post.user.name }}</p>
                <p class="user__account_name">@{{ post.user.username }}</p>
            </div>
        </a>
        <div class="img_container">
            <img :src="post.urls.regular" :alt="post.alt_description">
        </div>   
        <div class="views">
            <p>{{ post.likes }}</p>
            <img class="eye-icon" src="@/assets/icons/eye.svg" alt="">
        </div>
    </div>

</template>
<script>
export default {
    props: {
        posts: {
            type: Array,
            required: true
        },
        token: {
            type: String,
            required: true
        }
    }
}
</script>
<style scoped>
.post {
    background-color: #ffffff;
}
.img_container {
    position: relative;
    width: 100%;
    min-height: 230px;
    height: 71.875vw;
    overflow: hidden;
}
.img_container img {
    position: absolute;
    width: 100%;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    object-fit: cover;
}
.user {
    padding: 10px;
    background-color: #ffffff;
    display: flex;
    gap: 10px;
    align-items: center;
    height: 50px;
    width: 100%;
}
.user__profile_photo img{
    width: 100%;
}
.user__profile_photo {
    width: 30px;
    height: 30px;
    border-radius: 100%;
    overflow: hidden;
}
.user__name{
    color: #333333;
    font-size: 12px;
    font-weight: 700;
}
.user__account_name {
    color: #8D8D8D;
    font-size: 12px;
    font-weight: 400;
}
.views {
    padding: 11px 10px 17.53px;
    font-size: 12px;
    font-weight: 700;
    color: #8D8D8D;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    width: 100%;
    gap: 5px;
}
.eye-icon {
    height: 11.47px;
}
@media (min-width:480px) {
    .user{
        padding: 0;
    }
    .img_container{
        height: 62.500vw;
    }
}
@media (min-width:768px) {
    .post {
      
        padding: 0;
    }
    .user{
        padding: 10px;
    }
    .img_container{
        height: 29.948vw;
        height: 230px;
    }
}
@media (min-width:768px) {
    .img_container{
        height: 23vw;
    }
  }
</style>