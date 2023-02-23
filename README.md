# Hello-nci 

Setup
```
  mkdir hello-nci
  cd hello-nci/
  nix flake init -t github:yusdacra/nix-cargo-integration#simple-crate
```

Try dev shell
```
nix develop
```

Error message
```sample
error:
       … while evaluating the attribute 'optionalValue.value'

         at /nix/store/369wr4laqdqzh5brq1g7nfc1pbfh23sn-source/lib/modules.nix:775:5:

          774|
          775|     optionalValue =
             |     ^
          776|       if isDefined then { value = mergedValue; }

       … while evaluating a branch condition

         at /nix/store/369wr4laqdqzh5brq1g7nfc1pbfh23sn-source/lib/modules.nix:776:7:

          775|     optionalValue =
          776|       if isDefined then { value = mergedValue; }
             |       ^
          777|       else {};

       (stack trace truncated; use '--show-trace' to show the full trace)

       error: Failed while trying to navigate to ./ from /nix/store/8114r3y0paiwv5lwgr2yhgn5l3n89gal-source/
```

Repeat above to check its not a quirk of flakes needing git. 
```
git init
git add .
git commit -am "init. Rel path broken"
```
Same error as above. 

Edit the flake to comment out rel path.
```
hx flake.nix 
nix develop 
```
This now works.