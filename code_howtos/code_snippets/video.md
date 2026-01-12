# Video

## Basic Example Using only HTML
```html
<video id="experimentVideo" width="560" height="315" autoplay preload="auto" playsinline disablePictureInPicture >
    <source src="/dynamicAssets/videos/Experiments/MyExperiment/video.mp4" type="video/mp4">
</video>
```

## JS Example for More Control
Took this from the RateGest code. Requires the use of an outside library: https://github.com/sampotts/plyr

Add these to the top of the HTML file:
```html
<script
  src="https://cdnjs.cloudflare.com/ajax/libs/plyr/3.7.8/plyr.min.js"
  integrity="sha512-vONptKEoKbP1gaC5UkbYDa9OPr04ur4bxaaqT7DAJxGHB2oogtseCPrl5e5hPFokGYotlGNV4d+GM593ka7iNA=="
  crossorigin="anonymous"
  referrerpolicy="no-referrer"
></script>
<link rel="stylesheet" href="https://cdn.plyr.io/3.7.8/plyr.css" />
```

Then everything else is as expected, use `ng-init` to manage what happens on play, on end,
and disabling controls.
```html
<div id="experiment_body_1" class="panel-body" ng-init="RC.initializePlyr()">
  <div class="main" style="min-height: 660px">
    <div class="video-container">
      <div class="fade-toggle video-wrapper" ng-class="{ 'invisible': !showPlayer }">
        <video id="player" class="plyr__video-embed" crossorigin playsinline preload="auto"></video>
...
```
```js
this.initializePlyr = function () {
    $timeout(() => {
        if (self.questionIndex == 0) {
            $scope.src = $scope.videoBlob;
        }

        let player = new Plyr("#player", {
            autoplay: true,
        });

        player.source = {
            type: "video",
            sources: [
                {
                    src: $scope.src,
                    type: "video/mp4", // or appropriate MIME type
                },
            ],
        };

        player.on("ended", () => {
            player.controls = []; // Hide controls
            player.destroy(); // Optional: remove player completely
            $scope.$apply(() => {
                $scope.videoPlayed = true; // Optional UI message
                self.screen2 = true;
            });
        });

        player.on("play", () => {
            document
                .querySelector(".plyr__progress")
                ?.classList.add("hidden");
            document.querySelector(".plyr__time")?.classList.add("hidden");
        });

        // Optional: Prevent seeking via arrow keys
        document.addEventListener("keydown", (e) => {
            const keys = ["ArrowLeft", "ArrowRight", "Home", "End"];
            if (keys.includes(e.key)) {
                e.preventDefault();
            }
        });
    });
};
```
