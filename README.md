# RASE DB skeleton

| This repository contains the RASE DB skeleton for creating new databases for rapid inference of antibiotic resistance and susceptibility using RASE. Other components of the software include the [RASE pipeline](https://github.com/c2-d2/rase-pipeline/) and the [core RASE package](https://github.com/c2-d2/rase). For more information, see the [RASE paper](https://www.biorxiv.org/content/10.1101/403204v2) and the [RASE supplementary materials](https://github.com/c2-d2/rase-supplement/). |
|-|

## Creating a custom RASE DB

1. [Set up your computational environment.](https://github.com/c2-d2/rase-pipeline/blob/master/environment.md)

2. Create a repository for your DB on some git-based repository hosting service such as Github, Gitlab, or Bitbucket.

3. Run the following script in an empty directory. It will create a local git repository with with the RASE DB skeleton.

   ```
   /usr/bin/env bash -c "$(curl -fsSL https://raw.githubusercontent.com/c2-d2/rase-db-skeleton/master/init-repo.sh)"
   ```

4. Interconnect the local repository with the remote one. For Github, this could be done by
   ```
   git remote add origin git@github.com:your-github-id/your-db-repo.git
   git push -u origin master
   ```

5. Test that your computational environment is configured properly by constructing an example database:
   ```
   make && make cleanall
   ```

6. Modify the main configuration file `conf.mk`. In particular, update the DB name, the list of antibiotics and their corresponding breakpoints.

7. Place your input data or code for their download into `published/`. If some of the data are private, copy them to `unpublished/`.

8. Adjust code for preparing isolate whole-genome sequences in `isolates/`. Test it by running `make` inside the directory.

9. Adjust code for preparing the phylogenetic tree in `tree/`. Test it by running `make` inside the directory.

10. Adjust code for preparing the resistance data in `resistance/`. Test it by running `make` (or `make step1`, `make step2`, etc. for individual steps) inside the directory.

11. Construct the database by running `make` in the root directory. The constructed database then can be found in `_output`.

12. You can optionally plot MICs and resistance categories on a tree, and calculate prevalence of resistance phenotypes by `make plots`.

Now your code for building the database is ready. All the outputs can be removed by `make clean` or `make cleanall` (removes even downloaded source files), and regenerated by running `make` in the root directory.


## FAQs

> I have only S/I/R information rather than full MICs. How should I proceed?

Use fake MICs. For instance, you can use `0.0` for susceptible isolates, and `999.0` for resistant and intermediate ones.
