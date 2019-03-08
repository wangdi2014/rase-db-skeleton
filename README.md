# RASE DB skeleton

## Creating a custom RASE DB


1. Create a repository for your DB on some git-based repository hosting service such as Github, Gitlab, or Bitbucket.

2. Run the following script in an empty directory. It will create a local git repository with with the RASE DB skeleton.

   ```
   /usr/bin/env bash -c "$(curl -fsSL https://raw.githubusercontent.com/c2-d2/rase-db-skeleton/master/init-repo.sh)"
   ```

3. Interconnect the local repository with the remote one. For Github, this could be done by
   ```
   git remote add origin git@github.com:your-github-id/your-db-repo.git
   git push -u origin master
   ```

4. Test that your computational environment is configured properly by constructing an example database:
   ```
   make && make cleanall
   ```

5. Modify the main configuration file `conf.mk`. In particular, update the DB name, the list of antibiotics and their corresponding breakpoints.

6. Place your input data or code for their download into `published/`. If some of the data are private, copy them to `unpublished/`.

7. Adjust code for preparing isolate whole-genome sequences in `isolates/`. Test it by running `make` inside the directory.

8. Adjust code for preparing the phylogenetic tree in `tree/`. Test it by running `make` inside the directory.

9. Adjust code for preparing the resistance data in `resistance/`. Test it by running `make` (or `make step1`, `make step2`, etc. for individual steps) inside the directory.

10. Construct the database by running `make` in the root directory. The constructed database then can be found in `_output`.


## FAQs

> I have only S/I/R information rather than full MICs. How should I proceed?

Use fake MICs. For instance, you can use `0.0` for susceptible isolates, and `999.0` for resistant and intermediate ones.
