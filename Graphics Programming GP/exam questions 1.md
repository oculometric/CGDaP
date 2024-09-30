1. 
   a) texture mapping involves using an extra pair of coordinates (usually called U and V) to sample pixels from a 2D image and project it onto the surface of some geometry. this adds realism by creating much greater detail colour on a surface (without the need for extreme excessive geometry), and if normal/bump/roughness maps are used, different lighting behaviour across the surface as well, further altering the appearance of geometry across its surface **(2/2)**
   b) texture coordinates, usually called UV coordinates, are an extra set of coordinates given for each face corner (there may be more than one UV coordinate per vertex). these additional 2-dimensional coordinates represent where vertices appear on the 2D texture being applied, and are used to sample pixels from a texture which can then be applied as colour data to a 3D model. UV coordinates are interpolated between face corners using barycentric coordinates. **(2/3) mention where texture starts and ends, be more specific about that areas of the texture are mapped onto specific faces**
   c) firstly, a texture must be loaded, using the `glGenTextures`, `glBindTexture`, and `glTexImage2D` functions. then, when geometry is being drawn first `glBindTexture` should be used to set the active texture to the one desired, before each `glVertex3f` call (or similar), a call should be made to `glTexCoord2f` with the arguments being the X and Y position in the texture the vertex should sample from. **(3/5) remember to set texture parameters like wrapping and filtering mode, remember to enable textures**
   d) since rendering is happening on the GPU, textures are stored in buffers allocated by openGL. those texture buffers are identified by a number, the ID of the texture. this ID is given when calling `glGenTextures`, and can be used with the `glBindTexture` function to tell the GPU which buffer to sample from during subsequent drawing operations. the ID uniquely identifies the texture. **(2/2)**
   e) bilinear and quadratic are two filtering algorithms used to downsample textures in OpenGL. when objects are far away or small (and thus one pixel on the screen may cover multiple pixels in the texture applied to the object), some kind of filtering should be applied. without filtering, only the closest matching pixel in the texture would be sampled and applied to the screen buffer, leading to artefacts like aliasing, jagged edges and patterning. filtering textures involves taking multiple samples of the texture per pixel, and averaging the result, to reduce such artefacts. bilinear is a cheap, reasonably good looking option, while quadratic is a more computationally expensive, but much better looking option. **(1/3) bilinear interpolates texel colours from 4 nearest texels based on fragment position within the texel, providing smooth results. nearest neighbour simply samples the nearest texel which produces aliasing**
   f) mip-mapping involves storing multiple copies of a texture at once, at different downscaled resolutions. while it uses more memory than a single texture, it allows geometry where the texture appears visually very small (like small or far away objects) to have it's texture cheaply sampled at a lower resolution. this may reduce render time when there are many far-away objects, and helps to reduce artefacts like aliasing. **(3/3) GL selects the best one automatically, avoids overly sharp or blurry textures**
2. 
   a) model coordinates are position coordinates (XYZ) used to describe the position of vertices or other geometric features relative to the origin of a particular 3D model. this is useful since 3D models may be moved around, rotated, and scaled within the world. world coordinates describe features which are relative to the world (or scene) origin, which is always fixed. **(2/2) when being rendered, coordinates are first transformed into world space before being transformed into view space**
   b) `glMatrixMode` allows the code to switch between modifying two different matrix stacks, the projection and model-view matrix stacks (in this case, making the projection matrix active). it means that any subsequent calls which modify the current matrix, like `glTranslate` and `glRotate` (etc) will be applied to whichever matrix has just been switched to. having these two different stacks allows the matrix which transforms coordinates from model space into view space to be separate from the matrix which performs the projection transformation (view space into NDC). after switching to the projection matrix, one might make a call to `gluPerspective` to configure the projection matrix with a perspective transform, or `gluOrtho` to set it up with an orthographic transform. **(3/4) don't need to know why we have different stacks, projection matrix transforms 3D scene onto 2D viewplane, could also use glViewport, maps NDCs to window coords**
   c) when modifying the model-view matrix, you are able to modify the model-world and world-view transforms (since they will be applied as a single transformation to geometry). following this call, one would first apply transformations representing the inverse of the camera transform (i.e. configure the world-view matrix) and then call `glPushMatrix` to make a copy of the matrix on the top of the stack, before applying transformations representing those applied to individual objects (before drawing those objects); remembering that transformations are applied to geometry in the reverse order in which function calls are made due to the nature of matrix multiplication. **(3/4) explain what the model-world and world-view transforms are, name the functions used i.e. glTranslatef glRotatef**
   d) 
```
// assume the robot's forearm has been set up in a heirarchy which looks like this:
// root
//  -> forearm
//   -> hand
//    -> finger_1
//    -> finger_2
// this recursive function can be called with root as the initial argument to draw the heirarchy
void DrawHeirarchy(Object* obj)
{
	glMatrixMode(GL_MODELVIEW)
	glPushMatrix();

	glTranslatef(obj->position.x, obj->position.y, obj->position.z);
	glRotatef(obj->euler.y, 0.0f, 1.0f, 0.0f);
	glRotatef(obj->euler.x, 1.0f, 0.0f, 0.0f);
	glRotatef(obj->euler.z, 0.0f, 0.0f, 1.0f);
	glScalef(obj->scale.x, obj->scale.y, obj->scale.z);

	Draw(obj->geometry);

	for (Object* child : obj->children)
	{
		DrawHeirarchy(child);
	}

	glPopMatrix();
}
```
**(6/6)**
**(27/35) 77%**