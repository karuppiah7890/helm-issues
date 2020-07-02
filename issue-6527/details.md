Okay, so it's been around 8 months and I haven't made any progress in this PR.
🙈

I know the fix to the code. But the maintainers asked for a test.

One of the old PRs for the issue is here
https://github.com/helm/helm/pull/6523

We spoke about having tests that will run on windows to find out if the issue
is present or not.

Unfortunately, it seems to be a totally separate issue. I think we can just
add the code and think about how to bring in support for windows users.

I mean, I can already see the issue about `syscall.Umask` being undefined
for windows when I run test using `GOOS=windows`. It's weird that the last time
I used windows VM to try it out. I think first the build should work in Mac with
the env variable. And then I can see if the existing tests help with this issue,
to test the issue, or not. I believe at least one of them should help. Or I
could just add a bad template yaml to the test data and bring it in.

It's just that I need to fix this windows issue. Damn thing, I'm not really that
much fan of windows. Looks like there's no concept of file permissions over there
like Mac or Linux. I mean, it's not like `rwx` and all. I think it's different
over there, the way it's managed etc. So, the concept of permission bits won't
make sense there. And the code has some places where these permission bits
come into play.

I wonder how golang handles the `ioutils.WriteFile` function which takes up a
file permissions mode, in windows OS. I gotta check that.

---

The simplest thing I can think of is, first fix the issue related to
`syscall.Umask` and make sure the build and tests don't fail in a windows system!

---

Now I'm checking how to do conditional compilation to build only some files
and not build some files based on the platform, in this case, the OS, the windows
OS.

https://dave.cheney.net/2013/10/12/how-to-use-conditional-compilation-with-the-go-build-tool

https://golang.org/pkg/go/build/#hdr-Build_Constraints

I could move the `TestExtract` function alone to a separate file and make sure
it's not compiled for windows. But then that wouldn't get tested in windows
then.

pkg/plugin/installer/http_installer_test.go

---

I commented out the `syscall.Umask` function calls and made changes to the test
based on the functionality that it did, with respect to file permissions. And
the tests pass in my Mac Machine. Gotta check in Windows next!


