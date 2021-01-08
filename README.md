# Most_secure_encryption

There is one encrpytion that is 100% secure (if the key is not caught), even if the attacker has the best quantum super computer avaible. This method is also one of the simplest encrpytion methods. The keys consits of random bits, each bit of the message corresponds to exactly one bit of the key and no bit of the key is used for more than one bit of message. You send the XOR of the bit you want to encrypt and the key bit.

Example:

Key:            10100011...

Message 1:      0010

Enc. Message 1: 0010 XOR 1010 =1000

Message 2:          1111

Enc. Message 2:     1111 XOR 0011 =1100



If the end of the key is reached, a new key has to be exchanged (perferably in person, otherwise this method does not really make sense).

Usage:

One party has to generate the key and the other party has to receive the key. The "receiving" is necessary since the receiving party uses the second half of the key to encrypt messages and the program has to know which half to use. 



generate a key for [name of receiver]:			key -g [name of receiver] [number of characters]

The key is created in ~/.key. [name of receiver] is always needed as an argument if the generator of the key wants to encrypt or decrypt a message. Each user can encrypt [number of characters] with the generated key. Each character requires two key characters and the key consists of two parts, one for each user. This means that the size of the key is 4 times [number of characters]. Note that this program uses "urandom" to generate random bits and these are not secure. To have a 100% procent secure method, one needs better ways of creating random bits.



receive a key from [name of generator]:			key -r [name of generator] [key file]

The key the receiver gets from the generator is by default named key_[name of receiver]. This name is the name that the generator of the key gives as an argument when he encrypts or decrypts a message for/from the receiver. The receiver of the key does not need to know or use [name of receiver] in any way. [name of generator] is chosen by the receiver of the key and the receiver always has to give this chosen name as an argument when he encrypts or decrypts a message for/from the genetator of the key. The generator of the key does not need to know or use [name of generator] in any way. 'key -r [...]' will copy [key file] to ~/.key, modify it and name it key_[name of generator]. [key file] can be deleted afterwards.



encrypt the [file] for [name]:		key -e [name] [file] {path}

[name] is the name you chose for the user for whom the message is. This means it is [name of receiver] if you generated the corresponding key and [name of generator] if you received the key. Umlaute and 'ß' are replaced by 'ae',..., 'Ue' and 'ss' and all other non-ascii characters are ignrored. The output file is message_[name]_[some_number] in the current folder, or text to stdout if '-o' is given.



decrypt the [file] from [name]:	key -d [name] [file] {path}

The explanation is analogous to '-e'.



Do not edit the folder '~/.key'.

{path} is an optional argument. If it is given, the key and cnt file are expected to be in {path}. The default path is ~/.key.

If the option '-i' is given, treat the input as text instead of using a file.

If the option '-o' is given, output to stdout instead of creating a file.

