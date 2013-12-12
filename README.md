
0. download monthly .pnt files to /mnt/scratch/... on cloud0-a, and run script in that
   dir to convert to yearly average pnt files, then transfer results to
   data/yearly-avg-pnt-files in this dir.
   
1. Convert yearly avg files from pnt to pkz format in dir _data/yearly-avg-pkz-files_:
   ```
   mkdir data/yearly-avg-pkz-files
   ./pntcomp2/pnt-to-pkz -o data/yearly-avg-pkz-files data/yearly-avg-pnt-files
   ```
   
2. Compute 22-year running averages in dir _data/22year-running-averages_:
   ```
   ./pntcomp2/pkz-avg --count=22 --outfile-pattern="%s.pkz" --outdir=data/22year-running-averages `find data/yearly-avg-pkz-files -name '*.pkz' -print | sort`
   ```

3. 
* pkz-subtract

  Compute the difference of two pkz files.
  
* compute-22year-anomalies

  Compute the difference of each 22year running average pkz file in data/intermediate/22year-running-averages
  with the 1901-1960 average data/final/tavg-1901-1960.pkz 

* pkz-to-contour-json

  Load a single pkz file and generate a json contour file from it.

* jsonify-22year-anomalies

  Run pkz-to-contour-json on each pkz file found in data/final/22year-anomalies, generating
  the corresponding json file, which will also be stored in data/final/22year-anomalies.

* dopages

  Use phantomjs to render an image for each contour json file in data/final/22year-anomalies;
  store the images in data/final/22year-anomaly-images.

* generate-animated-gif

  Generate a single animated gif image from all the images found in data/final/22year-anomaly-images
