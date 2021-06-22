<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
        <div class="row">    
            <VideoDetail :video="selectedVideo" />
            <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
        </div>
    </div>
</template>

<script>
//imports
import SearchBar from './components/SearchBar';
import axios from 'axios';
import VideoList from './components/VideoList';
import VideoDetail from './components/VideoDetail';

//API Key to acces the youtube API
const API_KEY = '(Write here the API key of your API of YouTube, without the parenteses)';

export default{
    name: 'App',
    components: {
        SearchBar,
        VideoList,
        VideoDetail,
    },
    data() {
        return{ 
            videos: [],
            selectedVideo: null    
        };
    },

    methods: {
        onTermChange(searchTerm) {

            axios.get('https://www.googleapis.com/youtube/v3/search', {
                params: {
                    key : API_KEY,
                    type: 'video',
                    part: 'snippet',
                    q: searchTerm,
                }
            }).then(response => {
                this.videos = response.data.items;
            });
        },

        onVideoSelect(video){
            this.selectedVideo = video;
        }
    }
};
</script>
