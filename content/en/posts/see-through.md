---
title: "Simple See-Through Shader for 2D Sprites in 3D World"
date: 2018-04-11
author: "Clément Fazilleau"
draft: false
tags: [ Unity, Shader ]
description: a very simple 2D sprite shader for 3D rendering.
---
## Simple See-Through Shader for 2D Sprites in 3D World

I am currently making a game.This is quite simple, It’s a stealth game where the graphics are paper-mario like.So I had the choice: I could have used a 3D Plane with a material containing my texture, and mess around with only 3D objects, but there was still a problem with that: I wanted to use the simple animation of the unity 2D sprites.
What I chose was a 3D GameObject with a capsule collider, Rigidbody, Navmesh agent, etc.. AND a sprite renderer attached to him. So I am able to use a simple spritesheet for the animation system.
The problem came when I had to make the player slightly visible through walls (because, you know, stealth game…) I had to make a shader.

{{< zooom src="/see-through/see-through_01.jpg" >}}

The only experience I had so far with shaders was a vertex/fragment shader for OpenGL. The Unity shaders are quite different, so I had to learn a lot of new things. And most of the shaders on the internet are for 3D projects or 2D projects, but never for a mix of both.

### 1. A Basic Sprite Shader

I found [this basic sprite ](https://github.com/nubick/unity-utils/blob/master/sources/Assets/Scripts/Shaders/Sprites-Default.shader)shader on GitHub, it helped me a lot to understand how unity shaders works.

Basically, here’s the structure of a shader…

```C
Shader "<name>"
{
	<optional: Material properties>
	<One or more SubShader definitions>
	<optional: custom editor>
	<optional: fallback>
}
```

You can find more information about that [right here.](https://docs.unity3d.com/Manual/SL-Shader.html)

In our case, the syntax will look like this:

{{< zooom src="/see-through/see-through_02.jpg" >}}

We’ve got one subshader with two pass: one for the visible part of the sprite, and the other for the grey silhouette hidden by our 3D objects.

{{< zooom src="/see-through/see-through_03.jpg" >}}

We will also need two properties:

```C
Properties
{
	[HideInInspector]
	_MainTex    ("Sprite Texture", 2D)          = "white" {}
	_GhostColor ("See-through Color", Color)    = (0.2, 0.2, 0.2, 1)
}
```

we use that `[HideInInspector]` tag because we don’t want the user but the sprite renderer to tell the shader which texture to use, so we disallow the user to have access to it from the editor.

`_GhostColor` is the only property the user will have access to, in order to choose the color of the player’s *Ghost*.

The properties are defined, we can start to make our subshader!

### 2. SubShader

```
SubShader
{
  Tags
  {
    "Queue"="Transparent"
    "PreviewType"="Plane"
  }
```

we choose the render queue tag `Transparent` so it will be rendered after the other objects (but before the overlay)
we also set the `PreviewType` as a `Plane` because we want the material to appear as a sprite material in the editor.

[More informations about SubShader tags…](https://docs.unity3d.com/Manual/SL-SubShaderTags.html)

```
Cull    Off
Blend   One OneMinusSrcAlpha

CGINCLUDE
...
ENDCG

Pass
{
...
}

ZTest   Greater
ZWrite  Off

Pass
{
...
}

```

`Cull Off` will tell the shader to not use culling, so both sides of the sprite will be visible
`Blend One OneMinusSrcAlpha` will tell the shader to use alpha blending *aka transparency*.

`CGINGLUDE` is the *header* of all our future `CGPROGRAM` it is here to prevent us from duplicating code, it makes the code more readable.

you can also see that before the second `Pass` we have `ZTest Greater` which tell the shader to apply this program to only the parts that are greater on the Z-buffer (the hidden parts) and `ZWrite Off` which will prevent our sprites from hiding each others.

### 3. The Programs

```C
CGINCLUDE
#include "UnityCG.cginc"

sampler2D   _MainTex;
fixed4      _GhostColor;

struct appdata_t
{
  float4 vertex : POSITION;
  float4 color    : COLOR;
  float2 texcoord : TEXCOORD0;
};

struct v2f
{
  float4 vertex : SV_POSITION;
  fixed4 color    : COLOR;
  float2 texcoord : TEXCOORD0;
};
```

We first declare our global parameters corresponding to the properties of the shader (`_MainTex` and `_GhostColor`).

then we declare two structs, `appdata_t` for the vertex part of the shader and `v2f` for the fragment part.

{{< zooom src="/see-through/see-through_04.png" >}}

### 4. The Vertex Shader

```C
#pragma vertex vert
v2f vert(appdata_t IN)
{
  v2f OUT;
  OUT.vertex      = UnityObjectToClipPos(IN.vertex);
  OUT.texcoord    = IN.texcoord;
  OUT.color       = IN.color;
  return OUT;
}
ENDCG
```

`#pragma vertex vert` tells the shader to use the vert() function as the vertex part. the vertex part is only there to turn each element of your game into a projection on your 2D screen.
In the function we don't need to change the vertex UVs neither the vertex colors so we return the sames as the input ones.

the vertex shader is in the CGINCLUDE because it is the same for both of our `Pass` (shown part and hidden part)

### 5. The Fragment Shaders

```C
CGPROGRAM
#pragma fragment frag
fixed4 frag(v2f IN) : SV_Target
{
  fixed4 c = tex2D(_MainTex, IN.texcoord) * IN.color;
  c.rgb *= c.a;
  return c;
}
ENDCG
```

In the first fragment shader, all we do is output the fragment color corresponding to the texture and the alpha (Transparency).

```C
CGPROGRAM
#pragma fragment frag
fixed4 frag(v2f IN) : SV_Target
{
  fixed4 c = tex2D(_MainTex, IN.texcoord);
  return _GhostColor * _GhostColor.a * c.a;
}
ENDCG
```

For the hidden part, it's even easier, we return the `_GhostColor` processed with the alpha of the texture.

And that's all, really, we're done here!

{{< zooom src="/see-through/see-through_05.jpg" >}}

Full Script: [https://gist.github.com/cfazilleau/3a44f3f3af19e491e0b3cabcc65054b4](https://gist.github.com/cfazilleau/3a44f3f3af19e491e0b3cabcc65054b4)

------

<div align="center">A shader by Clément FAZILLEAU</div>