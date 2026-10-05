# Undo

## Challenge Information

- **Category:** General Skills
- **Difficulty:** Easy
- **Points:** 100
- **Event:** picoCTF
- **Year:** 2026

## Description

The challenge required reversing a series of Linux text transformations to recover the original flag.

## Objective

Connect to the challenge server and determine the correct Linux command to undo each transformation.

## Approach

I connected to the challenge using the provided Netcat command.

```bash
nc <IP> <PORT>
```

The server provided a transformed string and a hint for each step.

### Step 1

The first string was Base64 encoded.

```bash
base64 -d
```

### Step 2

The resulting text had been reversed.

```bash
rev
```

### Step 3

The underscores in the flag had been replaced with dashes.

```bash
tr '-' '_'
```

### Step 4

The curly braces had been replaced with parentheses.

```bash
tr '()' '{}'
```

### Step 5

The final transformation was ROT13.

```bash
tr 'a-zA-Z' 'n-za-mN-ZA-M'
```

## Solution

After reversing all five transformations, the server returned the original picoCTF flag.

## Flag

```text
picoCTF{Revers1ng_t3xt_Tr4nsf0rm@t10ns_3a939318}
```

## Tools Used

- Netcat
- `base64`
- `rev`
- `tr`

## Key Takeaways

- Learned how to reverse common Linux text transformations.
- Practiced using `base64`, `rev`, and `tr`.
- Learned how multiple transformations can be reversed one step at a time.
