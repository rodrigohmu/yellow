## Eu sou uma Yappie.

<div id="fullscreen-container" style="width: 100%; height: 400px;">
    <iframe id="video" width="100%" height="100%" src="https://www.youtube.com/embed/jYB822q4LMk" frameborder="0" allowfullscreen="true"></iframe>
</div>
<button id="fullscreen-btn">Tela inteira</button>
<script src="youtube.external.subtitle.js"></script>
<script src="subtitles.parser.min.js "></script>

<script>
var loadSRT = function(url, callback) {
    var httpRequest = new XMLHttpRequest();

    httpRequest.onreadystatechange = function() {
        if (httpRequest.readyState === XMLHttpRequest.DONE) {
            var subtitles = parser.fromSrt(httpRequest.responseText, true);

            for (var i in subtitles) {
                subtitles[i] = {
                    start : subtitles[i].startTime / 1000,
                    end   : subtitles[i].endTime / 1000,
                    text  : subtitles[i].text
                };
            }

            callback(subtitles);
        }
    };

    httpRequest.open('GET', url, true);
    httpRequest.send(null);
};



loadSRT('subs/Im_a_Yappie._ptbr.srt', function(subtitles) {
    var youtubeExternalSubtitle = new YoutubeExternalSubtitle.Subtitle(document.getElementById('video'), subtitles);
});

document.getElementById('fullscreen-btn').addEventListener('click', function(e) {
    var elem = document.getElementById('fullscreen-container');

    var openFullscreen = function() {
      if (elem.requestFullscreen) {
        elem.requestFullscreen();
      } else if (elem.mozRequestFullScreen) { /* Firefox */
        elem.mozRequestFullScreen();
      } else if (elem.webkitRequestFullscreen) { /* Chrome, Safari & Opera */
        elem.webkitRequestFullscreen();
      } else if (elem.msRequestFullscreen) { /* IE/Edge */
        elem.msRequestFullscreen();
      }
    };

    openFullscreen();
  });

</script>
