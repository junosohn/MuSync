<template>
    <div>
        <div>
            <span class="track-album-art"><img width="57" height="57" v-bind:src="track.trackAlbumArt"/></span>
            <span class="track-name">{{ shortenString(track.trackName) }}</span><br>
            <span class="track-artist">{{ shortenString(track.trackArtist) }}</span><br>
            <span class="track-duration">{{trackDuration}}</span>
        </div>
    </div>
</template>

<script>
    var SpotifyWebApi = require('spotify-web-api-js');
    var spotifyApi = new SpotifyWebApi();

    export default {
        props: {
            "track": Object
        },
        data() {
            return {
                "trackDuration": ""
            }
        },
        created() {
            this.convertMilliseconds();
        },
        methods: {
            convertMilliseconds() {
                // Convert track duration in milliseconds to minutes:seconds
                var min = Math.floor(this.track.trackDuration / 60000);
                var sec = ((this.track.trackDuration % 60000) / 1000).toFixed(0);
                this.trackDuration = min + ":" + (sec < 10 ? '0' : '') + sec;
            },
            shortenString(s) {
                // Take substring if string is too long to display in one line
                if (s.length > 45) {
                    return (s.substring(0,45) + "...");
                }
                else {
                    return s;
                }
            }
        }
    }
</script>

<style lang="scss" scoped>
    .track-album-art {
        float: left;
        vertical-align: text-top;
        padding-right: 8px;
    }

    .track-name {
        float: left;
        font-size: 10px;
        font-weight: bold;

    }

    .track-artist {
        float: left;
        font-size: 10px;
    }

    .track-duration {
        float: left;
        font-size: 7px;
    }
</style>
