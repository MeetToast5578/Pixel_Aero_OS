# How to add the image pack to Pixel_Aero_OS on GitHub

Because the connected GitHub text-file API does not accept these local PNG paths, the binary images still need to be uploaded using Git or the GitHub website.

## Option A — Git (recommended)

1. Clone `https://github.com/MeetToast5578/Pixel_Aero_OS.git` and open the working folder.
2. Extract this ZIP, then copy its `references/` and `wallpapers/` folders into the repository root. Keep the existing `docs/` and `plan.md` unchanged.
3. Run:

```bash
git add references wallpapers
git commit -m "docs: add Pixel Aero visual references and wallpaper concepts"
git push origin main
```

4. Verify the images and markdown reference index on GitHub.

## Option B — GitHub website

Use **Add file → Upload files** in the repository (or in each destination directory) to upload PNGs, then commit the changes. Git is easier for the complete set because it preserves directory structure.

The index markdown assumes it lives in the folder specified in this ZIP. All images are concepts; the final asset licensing still needs a decision.
