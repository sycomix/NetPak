## NetPak Test Content

This directory serves as test content for NetPak.Test.

### Inputs

The files in `Content` are packaged using the official UnrealPak that is included with UE4 and the resulting pak file is placed in `Paks/Input`. The content is packaged with different flags for different test scenarios, but is always the same content.

The naming of the pak files follows the scheme UEVersion-Order-Description.pak. Order is used to set order the files will be tested. Some examples:
* `427-0-Simple.pak` is packaged using Unreal version 4.27. 0 means it should be the first to be tested within this version. Simple describes that no additional args were passed to UnrealPak.
* `427-1-Compressed.pak` is packaged using Unreal version 4.27. 1 means it should be the second to be tested within this version. Compressed means the `-Compressed` arg was passed to UnrealPak.
* `427-2-Encrypted.pak` follows the same pattern, but has been encrypted by UnrealPak. There should be a text file with the same name - but with the extension `.key` - next to it containing the encryption key in hex format.
* `427-3-EncryptedCompressed.pak` is both encrypted and compressed. Again, there should be a key file next to it containing the encryption key.

The files are packaged using a response file with a single line similar to the following. You should always use absolute paths within a response file, which is why one is not included in the repo.

```
D:\FullPathToProject\NetPak\NetPak.Test\TestData\Content\** ../../../TestGame/Content/
```

### Outputs

This directory will also contain files generated by NetPak.Test.

`OutContent` will contain the output of the currently running test. It is used to extract files from a generated pak and compare them with the original files in `Content`. This directory is removed after each test. So it will not be present after a run unless you abort the run early.

`Paks/Output` will contain paks generated by the tests. Each file from `Paks/Input` will be read and have its contents written to a new file with the same name in `Paks/Output`. This file will not be binary equal to the original, but should output binary equal content files when extracted.