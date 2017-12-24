Part 4: Finally some code
--------------------

Implement this in C, Python and Go:


    global shared int i = 0

    main:
        spawn thread_1
        spawn thread_2
        join all threads (wait for them to finish)
        print i

    thread_1:
        do 1_000_000 times:
            i++
    thread_2:
        do 1_000_000 times:
            i--
            

### Delivery
In this exercise you must take advantage of the starter code found in the subdirectories corresponding to the three different programming languages. You must fill out the missing code and make sure your program is working before commiting and pushing the changes to your repository.

At last, you should create a new file called RESULT.md inside this directory explaining what happens and why. Remember to add, commit and push the new file.

