<!DOCTYPE html>
<html>
<head>
    <title>Reverse Words</title>
</head>
<body>
    <form method="post">
        <label for="word">Введите слово:</label><br>
        <input type="text" id="word" name="word"><br><br>
        <input type="submit" value="Подтвердить">
    </form>

    <?php
    function reverseWords($input) {
        $words = preg_split('/([\s,\.\'"\-]+)/', $input, -1, PREG_SPLIT_DELIM_CAPTURE | PREG_SPLIT_NO_EMPTY);
        $result = "";

        foreach ($words as $word) {
            $reversed = "";
            $punctuation = "";
            $lastChar = mb_substr($word, -1, 1, 'UTF-8');
            // Check for punctuation at the end of the word
            if (preg_match('/[.,;:!?]/u', $lastChar)) {
                $punctuation = $lastChar;
                $word = rtrim($word, $lastChar);
            }

            $wordLen = mb_strlen($word, 'UTF-8');
            for ($i = $wordLen - 1; $i >= 0; $i--) {
                $reversed .= mb_substr($word, $i, 1, 'UTF-8');
            }

            $result .= $reversed . $punctuation . " ";
        }

        return $result;
    }

    if (isset($_POST['word'])) {
        $input = $_POST['word'];
        $output = reverseWords($input);
        echo "<p>введенные данные: " . $input . " </br> Результат: " . $output . "</p>";
    }
    ?>
</body>
</html>
