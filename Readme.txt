Single species future pipeline

Open the pipeline "Single_Species_future_pipeline.Rmd" and the functions "SA_Markdown_Functions.Rmd"

Load packages in both files

Load the functions in the functions Markdown before calling them in the pipeline. Pipeline chunks are numbered and labeled steps 1 through 15 and referred to as such in the functions file. 
Note: loadBioclim() function does not work on my machine, so I access the pre-downloaded files from the RDS joint project folder. Save under folder "CHELSA" in your working directory and use workaround by Vivienne, lines 60 - 73. 
Same thing for wwf_ecoregions_get(), line 186 in the functions file, cannot get to work so I access the WWF shapefiles from RDS joint project folder and save them under the folder "WWF_Ecoregions" in working directory. 

Future functions (steps 13 through 15): 
future-modelled climate and environmental data was downloaded from CHELSA's HadGEM model for two time periods (years 2041 - 2060 and years 2061 - 2080) and for two climate severity scenarios (moderate, representative concentration pathway 4.5 and extreme, rcp 9.5). Find more info on http://chelsa-climate.org and the CMIP5 website (also see van Vuuren et al., 2011; Riahi et al., 2015).

You need to save each time period, and each scenario under a seperate path in your working directory. Specify those paths and file names in Step 13. For instance, with two time periods and two scenarios, I wrote four folders. Each folder should contain five TIF files, which contain the five bioclimatic layers we use. Then, crop the rasters to the extent of occurrence for all of those scenario - time period combinations, which will take some time. 

Run the fit() functions for Bioclim, GLM and RF (step 14) then build the ensembles by reading in saved predictions (step 15). Do these two steps 14 - 15 for each time period and climate scenario (e.g. four times if you have two time periods and two scenarios). When running the fitBC_future(), fitGLM_future(), fitRF_future() functions, species the future_predictors variable based on the scenario / time period raster file you previously cropped in step 13, and the scenario and pred_out_dir variables based on which time period and scenario you are running. Notice for pred_out_dir you also want to create a different folder for each model predictions (bioclim, glm, rf). In step 15, also modify the here::here and pattern input variables in the preds() function to match your scenario and time period. Modify the name of the ensemble model lines #567 and #576 so you don't overwrite your previous scenarios and you can plot several ensembles later on to compare them. Also modify the scenario, method, and out_dir input variables to the ensemble functions. 

Plotting the future: 

The chunk line #590 is only for basic visualization of one ensemble at a time. To combine several rasters onto the same plot, use the comboplot chunk below (line #603). The purple in the plot will show you the difference between both rasters, aka those areas where the species distribution varies based on climate severity and time period in the future. 

The crop chunk (#620) helps make a zoomed inset for particularly interesting regions. To crop the rasters I exported them and edited them in qGIS before reading them back (line #622). 

The final chunk, barcharts (#632) prepares a histogram of extent of occurrence (or range, if you will) of two selected species across time period and climate scenarios. This is for analysis purposes. 
