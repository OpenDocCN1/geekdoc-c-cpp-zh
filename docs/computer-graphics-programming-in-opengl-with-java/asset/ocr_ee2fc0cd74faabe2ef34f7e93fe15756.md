```
    // Compute the diffuse and specular contributions
    diffuse = pointLight_diffuse * objMat_diffuse * max(cos_theta, 0.0);
    specular = pointLight_specular * objMat_specular * pow(max(cos_phi, 0.0), objMat_shininess);
    }
    vec4 phong_color = ambient + diffuse + specular;
    return phong_color.rgb;
    }
```

![](bbox=[0.297, 0.271, 0.704, 0.615])

**Figure 16.5**
Output of Program 16.4, showing simple ray casting with lighting and shadows.

# ### 16.3.3 Non-Axis-Aligned Ray-Box Intersection

So far, our box has been limited to an orientation where its X, Y, and Z axes are parallel with the world axes. We now show how to include translation and rotation, so that we can orient the box however we wish. Applying translation and rotation on the box is conceptually similar to building a view matrix, as we did in Chapter 4, although the details are slightly different.

We start by making sure that our `box_mins` and `box_maxs` variables define a box shape that is centered at the origin. We also specify: