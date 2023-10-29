# byte's blender assets

I've been putting a lot of work into my personal blender asset library lately, and since all of it is CC-0 (public domain) I figured I'd go ahead and make it available for others to use if they want. I'm trying to attribute stuff anyway in the asset metadata (when I can find the source), but everything in this collection was made available as CC-0.

This project is still pretty new, so expect the organization of stuff to change. As such, if you do use this library, you'll probably want to append assets instead of linking them, since links are liable to break in future updates.

**This repo requires [Git LFS](https://git-lfs.com/)!**

## Modifications

Note that many assets in this library won't exactly match their specified source. Many of them have been cleaned up or optimized by me for my own purposes. Many of them have also been isolated out of larger collections into individual assets. If you want the original from the source, just go to the URL in the asset metadata.

## Naming conventions

Whenever possible (or whenever I remember to), I try to follow a consistent naming scheme for texture files, based on Unreal Engine's preferred naming scheme. Texture files will generally have the following format:

`T_ModelName_SubPart_maptype_2k.ext`

- `ModelName` is either the name of the model the texture is used in (for single-purpose textures) or the name of the material if it's a texture used in a generic material
- `SubPart` is optional and there may be multiple sub-layers depending on the complexity of the mesh (or material, though usually not an issue for materials).
- `maptype` is the kind of texture map, from the following list:
  - `albedo` - the albedo, or diffuse color, or basecolor, or whatever you want to call it color. I chose albedo because it's the most technically accurate for PBR rendering.
  - `norm_GL` or `norm_DX` - a normal map, in either OpenGL or DirectX format (they represent the green channel as the opposite direction of the other. blender uses OpenGL format, so nearly all of the textures in this collection should be `norm_GL`)
  - `spec` - a specular map. I normally try to avoid these since it's not always clear how they're intended to be used, and their existence usually (but not always) suggests use of an outdated non-PBR workflow, where the specular lighting is manually tweaked to try to approximate the right look, which sometimes ends up looking out of place in otherwise photorealistic scenes. Should generally be single-channel.
  - `roughness` - a roughness map. A map of the PBR roughness value. Not much to say here. Should generally be single-channel.
  - `height` - a single-channel heightmap. May be used for displacement or for bump mapping, or both. Should generally be single-channel.
  - `alpha` - a single-channel opacity map. May be used for fully translucent materials or for alpha clipping. Should generally be single-channel. Alpha information will often be included in another texture though.
  - `metallic` - a metalicity map. Same as roughness but for the metallic value. Should generally be single-channel.
  - `ao` - prebaked ambient occlusion. Usually just multiplied with the albedo since the Principled BSDF node doesn't have a dedicated AO input. Should generally be single-channel.
  - `ARM` - a channel-packed combination map for ambient occlusion, roughness, and metalicity, in the R, G, and B channels respectively. I generally try to use these wherever at least two of the three components are in use, since fewer texture files is easier to manage. They're easy to split up if needed though.
  - `emissive` - an emissive lighting map. Will generally be RGB, even for white emitters, since its use is less ambiguous that way.
  - `mask` - a catch-all for any kind of layery-masky-type thing. Generally used for switching between materials on a mesh, or switching between attributes within a material, or something like that. Alpha masks should be labeled with `alpha`.
  - `sss` - subsurface scattering map. Will generally be RGB.
  - or some more specialized map types, such as `thickness`, `curvature`, `position`, `fuzz`, `ID`, and so on. The ones above are the most common though.
- `2k` is the resolution. Textures should generally be square powers of two (or sometimes non-square powers of two, like 1k by 2k), so these will generally be `512`, `1k`, `2k`, or `4k`, but higher or lower resolutions might exist in some cases. This specific part of the naming convention is important because I use my own blender addon (link TBD) for importing material assets with different resolution textures in blender (without having to do "Something 1K" and "Something 2K" and so on for each material). Material assets generally use 1K maps by default, with higher resolution maps available in the same locations.
- `ext` is the file extension, of course. Everything except normal maps will generally be high-quality JPEGs to save space, since minimal JPEG artifacting generally doesn't cause problems for most types of maps. If you'd prefer a lossless PNG, check the asset source to see if the original used one.
