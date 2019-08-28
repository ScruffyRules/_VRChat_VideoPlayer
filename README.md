# _VRChat_VideoPlayer

This is the readme/help for `_VRChat_VideoPlayer` texture  
If you'd like help with this feel free to DM me on Discord (`ScruffyRules#0879`) or mention me in `#random-chat` in the Official VRChat Discord

## For World Creators
I've provided a [zip package here](https://github.com/ScruffyRules/_VRChat_VideoPlayer/raw/master/VRChat_VideoPlayer.zip) which contains a prefab you can drag and drop into your world.  

### How to setup
1. Drag the `_VRChat_VideoPlayer` prefab into your world
2. Put your VideoPlayer's RenderTexture into the Button's OnClick Object slot
3. Set the function to `RenderTexture.SetGlobalShaderProperty`
4. Set the function argument to `_VRChat_VideoPlayer`
5. You're done!

### Render Texture settings
I'd recommend setting your [RenderTexture](https://docs.unity3d.com/2017.4/Documentation/Manual/class-RenderTexture.html) to these settings:
* Width: 1280
* Height: 720
* Color Format: ARGB32
* Depth Buffer: No Depth Buffer
* sRGB: Enabled
* Clamp Mode: Repeat

### Stream Players
This currently doesn't support Stream Players because they can only output to a texture slot not a RenderTexture

## For Avatar Creators
You'll have to use a shader that supports it.

Supported Shaders:
* Currently no one xd

## For Shader Developers
**DO NOT** add a property for this name, it will override the RenderTexture.

You need to add this
```hlsl
sampler2D _VRChat_VideoPlayer;
float4 _VRChat_VideoPlayer_TexelSize;
```
and then to use it you need to do
```hlsl
if (_VRChat_VideoPlayer_TexelSize.z != 0) { // For optimisation
    float4 vrc_videoplayer = tex2D(_VRChat_VideoPlayer, i.uv); // Use your (Custom?) UVs
    if (vrc_videoplayer.a == 1) { // This says if you're in a world that supports it or not
        return vrc_videoplayer; // You can do anything with this, I usually add it after lighting
    }
}
```
