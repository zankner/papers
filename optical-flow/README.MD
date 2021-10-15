RAFT was a significant improvement over the state of the art for optical flow networks. 

### Correlation volumes
The main addition is the similarity comparison of all pairs of features between the first frame and second frame. Essentially, a set of features is extracted for each frame, and then a 4d correlation volume is constructed by comparing each feature in the first frame with every feature in the second frame. The correlations with the second frame are pooled to different scales, however the dimensions of the first frame are kept meaning that high resolution information is preserved. 

### Lookup operator
The lookup operator provides a method to find the similarity between a patch from frame 1 and an area from frame 2. For each coarse level of the correlation pyramids, given an estimate of the optical flow in each direction, we pool the similarities in a radius around the projected flow.

### Update operator
Use a recurrent network, in this case a GRU, to iteratively update a prediction of the optical flow. The input to the network is the correlations found from current flow estimate, the current flow estimate, and a context vector extracted from the first frame.

After N iterations of the update operator the final flow is predicted. This loss is then directly optimized by l<sub>1</sub> distance between predictions and ground truth with exponentially increasing weighting.