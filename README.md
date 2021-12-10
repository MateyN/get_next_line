<h1 align="center">
    Project - get_next_line
    <h4 align="center" style="width: 50%; margin: 2rem auto; font-weight: normal;"> 
    Function which returns a line read from a file descriptor.
    </h4>
</h1>

## Description

Calling the function ``char *get_next_line(int fd)`` in a loop will allow you to read the text
available on the file descriptor one line at a time until the end of it.

The file must be read line by line until he founds a new line (ASCII = '\n') and not more. Read all the file in one time isn't recommended this is why we use a global ``BUFFER_SIZE`` to set how many octet the function will read.

## Functions needed
- [malloc()](https://man7.org/linux/man-pages/man3/malloc.3.html), [free()](https://man7.org/linux/man-pages/man1/free.1.html)
- [read()](https://man7.org/linux/man-pages/man2/read.2.html)
- [ft_strchr()](https://github.com/MateyN/42libft/blob/master/libft/ft_strchr.c), [ft_strlen()](https://github.com/MateyN/42libft/blob/master/libft/ft_strlen.c), [ft_strdup()](https://github.com/MateyN/42libft/blob/master/libft/ft_strdup.c), [ft_substr()](https://github.com/MateyN/42libft/blob/master/libft/ft_substr.c), [ft_strjoin()](https://github.com/MateyN/42libft/blob/master/libft/ft_strjoin.c), [ft_strlcpy()](https://github.com/MateyN/42libft/blob/master/libft/ft_strlcpy.c)

## Step-by-step

### 1. Setup variables
For this function we need to use 2 importants variable:
- ``static char *buff``: A static variable is able to save the data passed to it even after the function is ended, this will allow us to re-use the data in it after a new call of the function.
- ``char *line``: Will be used to return it with the current value regarding the ``BUFFER_SIZE``.

### 2. Check if our ``file descriptor`` is valid
We check the ``BUFFER_SIZE`` and the ``file descriptor``.

### 3. We check if there is a new line in ``buff`` or if it's a ``NULL``.
The second ``if`` statement applies if there's a new line in ``buff`` or if it's ``NULL``. Because ``buff`` is first declared as ``NULL``.

Line is then returned with ``ft_return_line ()``.

We go ``ft_read_file ()``.

### 4. Read the file
3 variables are required:
- ``int res``: To store what we first read.
- ``char *temp``: To save data and swap it later.
- ``char buff[BUFFER_SIZE + 1]``: To use as string and + 1 for the '\0'.

``ft_read_file`` will read the buffer and store in ``res`` what we first read.
time.
- We then enter our main loop. The loop iterates as long as the ``res`` value is greater than zero. So as long as there is something to read
(res = 0 is EOF).
- ``buff[res] = '\0'`` to notify the end of the buff string.
- We then store all our buffer into a temporary buff to free ``save`` of all the remains. Then put everything back from ``temp`` to ``save``.
- We then look for the new line into ``save``, and return the remainder.
- Finally to end the loop, we keep reading until we find a new line or the EOF.

### 5. Check the line and return the value
``ft_return_line`` will free ``buff`` and return ``NULL`` if ``buff`` is empty (or EOF).
- Otherwise, we enter a loop where we go through ``buff`` with our counter ``i``, until we find a new line, or the end of ``buff``.
- If we found a new line, the counter will move to the next line and start reading the next time we call ``buff``.
- Then we substract the line from start to '\n', but keep in mind the lenght of the buff string.
- Finally, we fill the remainder to ``temp`` to free ``buff``, then refill it again. Line is then returned.
