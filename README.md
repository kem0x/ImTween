<h1 align="center">ImTween</h1>

<p align="center">A simple, small, dependency-free single header-file tweening\animation extension for <a href="https://github.com/ocornut/imgui">dear imgui</a>.</p>

<p align="center">
  <img src="https://user-images.githubusercontent.com/19430119/203398586-87229cea-1271-4820-ba05-c9410578aa8b.gif">
</p>

ImTween aims to implement [Tweening](https://en.wikipedia.org/wiki/Inbetweening) concept in under a simple and easy to use template class, for [dear imgui](https://github.com/ocornut/imgui).

If you are not familiar with [Tweening](https://en.wikipedia.org/wiki/Inbetweening), it is a concept of interpolating between two values over time. It is used in many places but the most common use case is animation.

## Usage:

Download the [ImTween.h](ImTween.h) file and include it in your project.

- `ImTween::Tween<T>`: returns a tween object that can be used to animate an undefined number of `std::tuple<T, T, T*>` in the form of `std::tuple { min, max, &value }`, supports all types that have `+=` and `-=` operators defined.

  - **Note**: T of the tween object is the T of the tuple so for example if your tween is of type `float` then your values must be of type `std::tuple<float, float, float*>)`.

- `OfType`: sets the type of the tween object, currently there's only one possible type that is `PingPong` which returns the value to it's `min` state when the condition is no longer met.

- `Speed`: sets the speed of how much the value is increased on each tick.

- `When`: sets the condition of the tween object.

- `OnComplete`: sets the callback function that is called when the `value` is equal to `max`.

- `Tick`: ticks the tween object, has to be called every frame.

### Example:

```cpp
   ImTween<float>::Tween(
       std::tuple { 50.0f, 100.0f, &settingsButtonWidth },
       std::tuple { 50.0f, 100.0f, &closeButtonWidth },
       std::tuple { 65.f, 115.f, &rectwidth })
       .OfType(ImTween<>::TweenType::PingPong)
       .Speed(8.0f)
       .When(
           [&]()
           {
               return settingsButtonIsHovered || closeButtonIsHovered;
           })
       .OnComplete( //Optional
           [&]()
           {
               // Do something when tween completes
           })
       .Tick();
```

## License:
ImTween is licensed under the MIT License, see [LICENSE](LICENSE) for more information.

Credits are appreciated but not required.