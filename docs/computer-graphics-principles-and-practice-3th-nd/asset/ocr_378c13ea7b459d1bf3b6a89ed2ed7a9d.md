# Chapter 27

# Materials and Scattering

# 27.1　Introduction

This chapter is about the way we model the interaction of light with objects. The first several sections are about the physics and mathematical representation of these interactions. At the end, we briefly discuss a software interface that’s well suited to the rendering we’ll do later.

The first step in our discussion is to limit consideration, for much of the chapter, to light-object interactions that occur at surfaces; late in the chapter we briefly discuss the volumetric interaction that occurs in things like fog and colored water, etc. All these interactions, when considered *locally* (e.g., “Where does the light arriving at this bit of surface end up going?”), are called **scattering**. Mirror reflection, for instance, is one very special kind of scattering; Lambertian reflection is another.

Scattering is a messy process. For many materials of interest, the physical features of the material are at a scale of just a few wavelengths of light, so diffraction effects matter. The interaction of light with materials is dependent on the chemistry of the materials—the degree to which the material is a conductor or insulator, and the distribution of electron-energy levels in the material, as we saw in Chapter 26—which is highly variable. And even for the simplest of rough materials, light interacts with the rough material in varied and complex ways. The result is that scattering code is messy. If you peek inside almost any renderer, the representation of scattering is either oversimplified or very messy.

# 27.2　Object-Level Scattering

Operational definitions, like Le Corbusier’s “A house is a machine for living,” have an intrinsic appeal: They get to the heart of a subject from the speaker’s point of view. From the point of view of a renderer, an **object** is a machine for converting an incoming light field into an outgoing one, through some kind of interaction that’s of no particular relevance to the renderer. The machine has a few useful properties, determined by the laws of physics: If we sum two incoming