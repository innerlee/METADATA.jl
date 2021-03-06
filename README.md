This is the official METADATA repo for the Julia package manager. See [manual section](http://docs.julialang.org/en/latest/manual/packages/) on packages for how to use the package manager to install and develop packages.


Please note our current policies for accepting entries into METADATA.jl:

1. New packages submitted for registration must have at least one tagged version.
2. The lowest package version that will be accepted is v0.0.1. v0.0.0 is no longer permitted.
3. All new tagged versions of packages must have a `REQUIRE` file, which must at a minimum contain a single line like
   ```
   julia 0.3
   ```
   specifying a minimum version of Julia the package is expected to run on. Running `Pkg.tag` copies the contents of a package's `REQUIRE` file into `METADATA.jl/PkgName/versions/1.2.3/requires`.

   A common mistake is to have an entry of the form
   ```
   julia 0.3-
   ```
   with the intention of specifying "version 0.3 and up." On the contrary, this line means "at least a 0.3 pre-release julia."
4. New package version tags must have a minimum Julia version of `0.3` or newer. `0.3-` (0.3 pre-releases) is no longer allowed.
   Exceptions may be granted for `julia 0.2` if package authors are willing to vouch that they still test that their packages work on 0.2.
5. If your package works with Julia 0.4 but not 0.3, then specify `julia 0.4` in your `REQUIRE` file. If the package has had any previous tags which supported `julia 0.3`, then be sure to change the minor or major version number of the package via `Pkg.tag("PkgName", :minor)` for the first tag that no longer supports `julia 0.3`. This makes it possible to create a separate branch for any future bugfix releases that may be needed for the package on Julia 0.3.
6. We strongly encourage everyone to update METADATA.jl through pull requests, which can be generated for you automatically when using `Pkg.publish()`. GitHub's pull requests allow us to run basic checks on the metadata entries. All developers (especially experienced developers!) are strongly discouraged from editing METADATA.jl directly unless absolutely necessary.

These policies have been the result of many months of discussion to improve the quality of registered packages and the overall user experience with Julia packages.
