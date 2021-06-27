{:title "The Beauty of Code"
 :layout :post
 :klipse true
 :tags  ["clojure" "nature" "reflection"]}

Those who followed me in the past know that this isn't my first blog. About a year ago,
I realized that I wanted to share the joy that I experienced when programming. I wrote a few articles,
published even fewer, and then stopped. I asked myself why, and what I realized was that
I focused too much on getting readers and writing about "hot" topics that I stopped enjoying what I was doing.
Eventually, I stopped having motivation and abandoned both programming and writing altogether.

But after getting acquainted with [Clojure](https://clojure.org/) a few weeks back, I started 
feeling the same sense of joy I had when I first wrote my "Hello, World!" computer program back
in university. I guess coming from a strictly OOP background, having experienced functional programming
for the first time allowed me to reevaluate what I felt about programming in general. This is when I decided to write again.

So this blog is about me, trying to write once again, hoping that I get to stick to writing for the purest of reasons:
to share with everyone the beauty of code. In that vein, here's a [fractal tree](https://natureofcode.com/book/chapter-8-fractals/). It's one of the first "mathematical art" I learned how to code, inspired by one of my heroes Daniel Shiffman, author of [The Nature of Code](https://natureofcode.com/).

<div class="canvas-container">
  <canvas id="canvas"></canvas>
</div>

This blog will be littered with stuff similar to this, as well as more practical stuff in the realm of programming. I hope you enjoy the ride, friend :)

<div style="text-align: right">
<strong>&mdash; Adrian Perea</strong>
</div>

*P.S. You can modify the code below to alter the fractal! Try modifying the values of `fractal-height` and `theta`!*

```klipse-cljs
(defn get-canvas-container [id]
  (let [containers (js/document.getElementsByClassName "canvas-container")]
    (nth (array-seq containers) 0)))

(def container (get-canvas-container 0))
(def width (.-clientWidth container))
(def height (.-clientHeight container))

(def canvas (js/document.getElementById "canvas"))
(set! (.-width canvas) width)
(set! (.-height canvas) height)
(def ctx (.getContext canvas "2d"))

(defn branch [len theta]
  (.moveTo ctx 0 0)
  (.lineTo ctx 0 (- len))
  (.translate ctx 0 (- len))
  (set! (.-lineWidth ctx) 0.5)
  (set! (.-strokeStyle ctx) "#8A8A8A")
  (set! (.-fillStyle ctx) "rgba(1, 1, 1, 0)")
  (.stroke ctx)

  (let [shortened-len (* len 0.66)]
    (if (> shortened-len 3)
      (do
        (.save ctx)
        (.rotate ctx theta)
        (branch shortened-len theta)
        (.restore ctx)

        (.save ctx)
        (.rotate ctx (- theta))
        (branch shortened-len theta)
        (.restore ctx))
      (do
        (.arc ctx 0 (- len) 2 0 (* 2 Math/PI))
        (set! (.-strokeStyle ctx) "rgba(1, 1, 1, 0)")
        (set! (.-fillStyle ctx) "#BE0029")
        (.fill ctx)))))

(defn draw [len theta]
  (.beginPath ctx)
  (.translate ctx (/ width 2) height)
  (branch len theta))

;; try changing the values of `fractal-height` and `theta`
(def fractal-height (int (/ height 3)))
(def theta (/ Math/PI 7))
(draw fractal-height theta)
```
