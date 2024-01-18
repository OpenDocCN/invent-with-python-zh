# 十六、反转棋 AI 模拟

> 原文：[`inventwithpython.com/invent4thed/chapter16.html`](https://inventwithpython.com/invent4thed/chapter16.html)
> 
> 译者：[飞龙](https://github.com/wizardforcel)
> 
> 协议：[CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)

![image](img/6af76fd8abfbd0bb89d63623e52c2692.png)

来自第 15 章的反转棋 AI 算法很简单，但几乎每次我玩都会被它打败。因为计算机可以快速处理指令，它可以轻松地检查棋盘上的每个可能位置并选择得分最高的移动。用这种方式找到最佳移动需要我花费很长时间。

反转棋程序有两个函数，`getPlayerMove()` 和 `getComputerMove()`，它们都以格式 `[x, y]` 的两项列表返回所选的移动。这两个函数还具有相同的参数，游戏棋盘数据结构和一种类型的棋子，但返回的移动来自不同的来源——玩家或反转棋算法。

当我们用对 `getPlayerMove()` 的调用替换为对 `getComputerMove()` 的调用时会发生什么？然后玩家就不必输入移动；移动已经为他们决定好了。计算机正在与自己对战！

在本章中，我们将制作三个新程序，其中计算机将与自己对战，每个程序都基于第 15 章中的反转棋程序：

+   模拟 1：*AISim1.py* 将对 *reversegam.py* 进行更改。

+   模拟 2：*AISim2.py* 将对 *AISim1.py* 进行更改。

+   模拟 3：*AISim3.py* 将对 *AISim2.py* 进行更改。

从一个程序到下一个程序的微小更改将向您展示如何将“玩家对计算机”游戏转变为“计算机对计算机”的模拟。最终的程序 *AISim3.py* 与 *reversegam.py* 共享大部分代码，但目的完全不同。该模拟不让我们玩反转棋，而是教会我们更多关于游戏本身的知识。

您可以自己键入这些更改，也可以从书籍网站[*https://www.nostarch.com/inventwithpython/](https://www.nostarch.com/inventwithpython/)*下载它们。

**本章涵盖的主题**

+   模拟

+   百分比

+   整数除法

+   `round()` 函数

+   计算机对战游戏

### 让计算机自己对战

我们的 *AISim1.py* 程序将进行一些简单的更改，以便计算机与自己对战。`getPlayerMove()` 和 `getComputerMove()` 函数都接受一个棋盘数据结构和玩家的棋子，然后返回要进行的移动。这就是为什么 `getComputerMove()` 可以替换 `getPlayerMove()` 而程序仍然能正常工作。在 *AISim1.py* 程序中，`getComputerMove()` 函数被调用来代替 `X` 和 `O` 玩家。

我们还使程序停止打印进行的移动的游戏板。由于人类无法像计算机那样快速阅读游戏板，因此打印每一步并不有用，因此我们只在游戏结束时打印最终的游戏板。

这些只是对程序的最小更改，因此它仍会说诸如“玩家将先行。”之类的话，即使计算机正在扮演计算机和玩家的角色。

#### 模拟 1 的示例运行

当用户运行 *AISim1.py* 程序时，用户看到的内容如下。玩家输入的文本是粗体。

```py
Welcome to Reversegam!
The computer will go first.
  12345678
 +--------+
1|XXXXXXXX|1
2|OXXXXXXX|2
3|XOXXOXXX|3
4|XXOOXOOX|4
5|XXOOXXXX|5
6|XXOXOXXX|6
7|XXXOXOXX|7
8|XXXXXXXX|8
 +--------+
  12345678
X scored 51 points. O scored 13 points.
You beat the computer by 38 points! Congratulations!
Do you want to play again? (yes or no)
no
```

#### 模拟 1 的源代码

将旧的 *reversegam.py* 文件另存为 *AISim1.py* 如下：

1.  选择 **文件** ![image](img/6213f577c15feb006bdab7161d1cfc75.png) **另存为**。

1.  将此文件另存为 *AISim1.py*，以便您可以在不影响 *reversegam.py* 的情况下进行更改。(此时，*reversegam.py* 和 *AISim1.py* 仍具有相同的代码。)

1.  对 *AISim1.py* 进行更改并保存该文件以保留任何更改。(*AISim1.py* 将有新更改，*reversegam.py* 将保持原始的未更改的代码。)

这个过程将创建一个我们的反转棋源代码的副本作为一个新文件，你可以对其进行更改，同时保持原始的反转棋游戏不变（你可能想再玩一次来测试它）。例如，将*AISim1.py*中的第 216 行更改为以下内容（更改部分用粗体标出）：

```py
                move = getComputerMove(board, playerTile)
```

现在运行程序。请注意，游戏仍然会询问你是否想成为*X*还是*O*，但不会要求你输入任何移动。当你用`getComputerMove()`函数替换`getPlayerMove()`函数时，你不再调用任何从玩家那里获取输入的代码。玩家在原始计算机的移动后仍然按 ENTER 键（因为在第 232 行有`input('Press Enter to see the computer\'s move.')`），但游戏会自己进行！

![image](img/b4e69b1df0320a5805abf50d4a776e32.png)

让我们对*AISim1.py*进行一些其他更改。更改以下粗体标记的行。更改从第 209 行开始。这些更改大多数只是*注释掉*代码，这意味着将代码转换为注释，以便它不会运行。

如果在输入此代码后出现错误，请使用在线差异工具比较你输入的代码和书中的代码，网址为[`www.nostarch.com/inventwithpython#diff`](https://www.nostarch.com/inventwithpython#diff)。

`AISim1.py`

```py
        elif turn == 'player': # Player's turn
            if playerValidMoves != []:
                #if showHints:
                #    validMovesBoard = getBoardWithValidMoves(board,
                            playerTile)
                #    drawBoard(validMovesBoard)
                #else:
                #    drawBoard(board)
                #printScore(board, playerTile, computerTile)

                move = getComputerMove(board, playerTile)
                #if move == 'quit':
                #    print('Thanks for playing!')
                #    sys.exit() # Terminate the program.
                #elif move == 'hints':
                #    showHints = not showHints
                #    continue
                #else:
                makeMove(board, playerTile, move[0], move[1])
            turn = 'computer'

        elif turn == 'computer': # Computer's turn
            if computerValidMoves != []:
                #drawBoard(board)
                #printScore(board, playerTile, computerTile)

                #input('Press Enter to see the computer\'s move.')
                move = getComputerMove(board, computerTile)
                makeMove(board, computerTile, move[0], move[1])
            turn = 'player'



print('Welcome to Reversegam!')

playerTile, computerTile = ['X', 'O'] #enterPlayerTile()
```

#### 去除玩家提示，添加电脑玩家

如你所见，*AISim1.py*程序与原始的反转棋程序基本相同，只是我们用`getComputerMove()`替换了`getPlayerMove()`的调用。我们还对打印到屏幕的文本进行了一些更改，以使游戏更容易跟踪。当你运行程序时，整个游戏在不到一秒的时间内就完成了！

再次，大部分的更改只是将代码注释掉。由于计算机是在自己对弈，程序不再需要运行代码来获取玩家的移动或显示棋盘的状态。所有这些都被跳过，所以棋盘只在游戏的最后才显示。我们注释掉代码而不是删除它，因为如果需要以后重用代码，通过取消注释来恢复代码更容易。

我们注释掉了 209 到 214 行，因为我们不需要为玩家绘制游戏棋盘，因为他们不会玩游戏。我们还注释掉了 217 到 223 行，因为我们不需要检查玩家是否输入`quit`或切换提示模式。但是我们需要将 224 行向右缩进四个空格，因为它在我们刚刚注释掉的`else`块中。229 到 232 行也为玩家绘制游戏棋盘，所以我们也注释掉了这些行。

唯一的新代码在第 216 行和 241 行。在第 216 行，我们只是用`getComputerMove()`替换了`getPlayerMove()`的调用，如前所述。在 241 行，我们不再询问玩家是否想成为*X*还是*O*，而是始终将`'X'`分配给`playerTile`，将`'O'`分配给`computerTile`。（尽管这两个玩家都由计算机扮演，所以如果你愿意，你可以将`playerTile`重命名为`computerTile2`或`secondComputerTile`。）现在我们让计算机自己对弈，我们可以继续修改我们的程序，使其做更有趣的事情。

### 让电脑自己玩几次

如果我们创建了一个新的算法，我们可以将其与`getComputerMove()`中实现的 AI 进行比较，看看哪一个更好。然而，在这样做之前，我们需要一种评估玩家的方法。我们不能仅仅根据一场比赛来评估哪个 AI 更好，所以我们应该让 AI 们多次对弈。为此，我们将对源代码进行一些更改。按照以下步骤制作*AISim2.py*：

1.  选择**文件**![image](img/6213f577c15feb006bdab7161d1cfc75.png)**另存为**。

1.  将此文件另存为*AISim2.py*，这样你就可以在不影响*AISim1.py*的情况下进行更改。（此时，*AISim1.py*和*AISim2.py*仍然具有相同的代码。）

#### 模拟 2 的示例运行

当用户运行*AISim2.py*程序时，他们看到的是这样的。

```py
Welcome to Reversegam!
#1: X scored 45 points. O scored 19 points.
#2: X scored 38 points. O scored 26 points.
#3: X scored 20 points. O scored 44 points.
#4: X scored 24 points. O scored 40 points.
#5: X scored 8 points. O scored 56 points.
--snip--
#249: X scored 24 points. O scored 40 points.
#250: X scored 43 points. O scored 21 points.
X wins: 119 (47.6%)
O wins: 127 (50.8%)
Ties:   4 (1.6%)
```

由于算法包含随机性，你的运行结果不会完全相同。

#### 模拟 2 的源代码

更改*AISim2.py*中的代码以匹配以下内容。确保按照数字顺序逐行更改代码。如果在输入此代码后出现错误，请使用在线 diff 工具将你输入的代码与书中的代码进行比较，网址为[`www.nostarch.com/inventwithpython#diff`](https://www.nostarch.com/inventwithpython#diff)。

`AISim2.py`

```py
            turn = 'player'

NUM_GAMES = 250
xWins = oWins = ties = 0
print('Welcome to Reversegam!')

playerTile, computerTile = ['X', 'O'] #enterPlayerTile()

for i in range(NUM_GAMES): #while True:
    finalBoard = playGame(playerTile, computerTile)

    # Display the final score.
    #drawBoard(finalBoard)
    scores = getScoreOfBoard(finalBoard)
    print('#%s: X scored %s points. O scored %s points.' % (i + 1,
           scores['X'], scores['O']))
    if scores[playerTile] > scores[computerTile]:
        xWins += 1 #print('You beat the computer by %s points!
               Congratulations!' % (scores[playerTile] -
               scores[computerTile]))
    elif scores[playerTile] < scores[computerTile]:
        oWins += 1 #print('You lost. The computer beat you by %s points.'
               % (scores[computerTile] - scores[playerTile]))
    else:
        ties += 1 #print('The game was a tie!')

    #print('Do you want to play again? (yes or no)')
    #if not input().lower().startswith('y'):
    #    break

print('X wins: %s (%s%%)' % (xWins, round(xWins / NUM_GAMES * 100, 1)))
print('O wins: %s (%s%%)' % (oWins, round(oWins / NUM_GAMES * 100, 1)))
print('Ties:   %s (%s%%)' % (ties, round(ties / NUM_GAMES * 100, 1)))
```

如果这让你感到困惑，你可以随时从书的网站[`www.nostarch.com/inventwithpython/`](https://www.nostarch.com/inventwithpython/)下载*AISim2.py*源代码。

#### 跟踪多场比赛

模拟中我们想要的主要信息是在一定数量的比赛中*X*的获胜次数、*O*的获胜次数和平局次数。这些可以在第 237 和 238 行创建的四个变量中进行跟踪。

```py
NUM_GAMES = 250
xWins = oWins = ties = 0
```

常量`NUM_GAMES`确定计算机将玩多少场比赛。你已经添加了变量`xWins`、`oWins`和`ties`来跟踪*X*赢得比赛、*O*赢得比赛和平局的次数。你可以将赋值语句链接在一起，将`ties`设置为`0`，`oWins`设置为`ties`，然后将`xWins`设置为`oWins`。这将把这三个变量都设置为`0`。

`NUM_GAMES`在`for`循环中使用，取代了第 243 行的游戏循环：

```py
for i in range(NUM_GAMES): #while True:
```

`for`循环运行了`NUM_GAMES`次游戏。这取代了以前循环直到玩家表示不想再玩另一场比赛的`while`循环。

在第 250 行，一个`if`语句比较了两个玩家的得分，而在`if-elif-else`块的 251 到 255 行中，在每场比赛结束后递增了`xWins`、`oWins`和`ties`变量。

```py
    if scores[playerTile] > scores[computerTile]:
        xWins += 1 #print('You beat the computer by %s points!
               Congratulations!' % (scores[playerTile] -
               scores[computerTile]))
    elif scores[playerTile] < scores[computerTile]:
        oWins += 1 #print('You lost. The computer beat you by %s points.'
               % (scores[computerTile] - scores[playerTile]))
    else:
        ties += 1 #print('The game was a tie!')
```

我们注释掉了最初在代码块中打印的消息，现在每场比赛只打印得分的一行摘要。我们将在代码的后面使用`xWins`、`oWins`和`ties`变量来分析计算机之间的表现。

#### 注释掉 print()函数调用

你还注释掉了 247 行和 257 到 259 行。通过这样做，你从程序中删除了大部分`print()`函数调用，以及对`drawBoard()`的调用。我们不需要看到每场比赛，因为比赛太多了。程序仍然完整地运行每场比赛，使用我们编写的 AI，但只显示结果得分。在运行所有比赛后，程序会显示每一方赢得了多少场比赛，251 到 253 行打印了一些关于比赛运行的信息。

向屏幕打印东西会减慢计算机的速度，但现在你已经删除了那些代码，计算机可以在大约一两秒内运行完整的反转棋游戏。每次程序打印出最终得分的那一行时，它都会运行整个游戏（逐个检查大约 50 到 60 个移动，选择得分最高的那个）。现在计算机不需要做太多工作，它可以运行得更快。 

程序在最后打印的数字是*统计数据*——用于总结比赛过程的数字。在这种情况下，我们展示了每场比赛的结果得分以及每个方块的胜利和平局的百分比。

#### 使用百分比来评估 AI

*百分比*是总量的一部分。整体的百分比可以从 0%到 100%不等。如果你有整个馅饼的 100%，你将拥有整个馅饼；如果你有 0%的馅饼，你将一点馅饼都没有；如果你有馅饼的 50%，你将拥有一半。

我们可以用除法来计算百分比。要获得百分比，将你拥有的部分除以总数，然后乘以 100。例如，如果*X*赢得了 100 场比赛中的 50 场，你将计算表达式`50/100`，其结果为`0.5`。将这个数乘以`100`就得到了百分比（在这种情况下是 50%）。

如果*X*在 200 场比赛中赢了 100 场，你可以用`100 / 200`来计算百分比，这也等于`0.5`。当你将`0.5`乘以`100`来得到百分比时，你会得到 50%。赢得 200 场比赛中的 100 场与赢得 100 场比赛中的 50 场是相同的百分比（即相同的部分）。

在 261 到 263 行，我们使用百分比来打印有关比赛结果的信息：

```py
print('X wins: %s (%s%%)' % (xWins, round(xWins / NUM_GAMES * 100, 1)))
print('O wins: %s (%s%%)' % (oWins, round(oWins / NUM_GAMES * 100, 1)))
print('Ties:   %s (%s%%)' % (ties, round(ties / NUM_GAMES * 100, 1)))
```

每个`print()`语句都有一个标签，告诉用户打印的数据是*X*赢得、*O*赢得还是平局。我们使用字符串插值来插入赢得或平局的比赛次数，然后插入赢得或平局占总比赛的百分比，但你可以看到我们不是简单地将`xWins`、`oWins`或`ties`除以总比赛次数并乘以`100`。这是因为我们希望每个百分比只打印一位小数，这是我们无法用普通除法做到的。

##### 除法求值为浮点数

当你使用除法运算符(`/`)时，表达式将总是求值为浮点数。例如，表达式`10 / 2`求值为浮点数值`5.0`，而不是整数值`5`。

这很重要要记住，因为使用`+`加法运算符将整数添加到浮点数值时，结果也总是求值为浮点数值。例如，`3 + 4.0`求值为浮点数值`7.0`，而不是整数`7`。

将以下代码输入到交互式 shell 中：

```py
>>> spam = 100 / 4
>>> spam
25.0
>>> spam = spam + 20
>>> spam
45.0
```

在这个例子中，`spam`中存储的值的数据类型始终是浮点数值。你可以将浮点数值传递给`int()`函数，该函数返回浮点数值的整数形式。但这将总是将浮点数值向下舍入。例如，表达式`int(4.0)`，`int(4.2)`和`int(4.9)`都会求值为`4`，而不是`5`。但在*AISim2.py*中，我们需要将每个百分比四舍五入到十分位。由于我们不能简单地进行除法，我们需要使用`round()`函数。

##### round()函数

`round()`函数将浮点数四舍五入到最接近的整数。将以下内容输入到交互式 shell 中：

```py
>>> round(10.0)
10
>>> round(10.2)
10
>>> round(8.7)
9
>>> round(3.4999)
3
>>> round(2.5422, 2)
2.54
```

`round()`函数还有一个可选的第二个参数，你可以指定要将数字舍入到的位置。这将使舍入后的数字成为浮点数，而不是整数。例如，表达式`round(2.5422, 2)`求值为`2.54`，`round(2.5422, 3)`求值为`2.542`。在*AISim2.py*的 261 到 263 行，我们使用带有参数`1`的`round()`来找到*X*和*O*赢得或平局的比赛的百分比，直到小数点后一位，这给我们准确的百分比。

### 比较不同的 AI 算法

只需做一些改动，我们就可以让计算机自己玩数百场比赛。现在，每个玩家赢得大约一半的比赛，因为两者都完全相同的算法进行移动。但如果我们添加不同的算法，我们可以看到不同的 AI 是否会赢得更多比赛。

让我们添加一些新的带有新算法的函数。但首先，在*AISim2.py*中选择**文件**![image](img/6213f577c15feb006bdab7161d1cfc75.png)**另存为**，将这个新文件保存为*AISim3.py*。

我们将`getComputerMove()`函数重命名为`getCornerBestMove()`，因为这个算法首先尝试在角落移动，然后选择翻转最多瓷砖的移动。我们将称这种策略为*角落最佳算法*。我们还将添加其他几个实现不同策略的函数，包括一个*最差移动算法*，它得到最低分的移动；一个*随机移动算法*，它得到任何有效的移动；以及一个*角边最佳算法*，它与角落最佳 AI 相同，只是在角落移动后寻找边移动，然后再进行最高分的移动。

在*AISim3.py*中，第 257 行对`getComputerMove()`的调用将被更改为`getCornerBestMove()`，第 274 行的`getComputerMove()`将变为`getWorstMove()`，这是我们将为最差移动算法编写的函数。这样，我们将有常规的角落最佳算法与一个故意选择翻转*最少*棋子的移动的算法对抗。

#### 模拟 3 的源代码

当您将*AISim3.py*的源代码输入到已重命名的*AISim2.py*的副本中时，请确保按照数字顺序逐行编写代码，以便行号匹配。如果在输入此代码后出现错误，请使用[`www.nostarch.com/inventwithpython#diff`](https://www.nostarch.com/inventwithpython#diff)上的在线差异工具将您输入的代码与书中的代码进行比较。

`AISim3.py`

```py
def getCornerBestMove(board, computerTile):
--snip--
def getWorstMove(board, tile):
    # Return the move that flips the least number of tiles.
    possibleMoves = getValidMoves(board, tile)
    random.shuffle(possibleMoves) # Randomize the order of the moves.

    # Find the lowest-scoring move possible.
    worstScore = 64
    for x, y in possibleMoves:
        boardCopy = getBoardCopy(board)
        makeMove(boardCopy, tile, x, y)
        score = getScoreOfBoard(boardCopy)[tile]
        if score < worstScore:
            worstMove = [x, y]
            worstScore = score

    return worstMove

def getRandomMove(board, tile):
    possibleMoves = getValidMoves(board, tile)
    return random.choice(possibleMoves)

def isOnSide(x, y):
    return x == 0 or x == WIDTH - 1 or y == 0 or y == HEIGHT - 1

def getCornerSideBestMove(board, tile):
    # Return a corner move, a side move, or the best move.
    possibleMoves = getValidMoves(board, tile)
    random.shuffle(possibleMoves) # Randomize the order of the moves.

    # Always go for a corner if available.
    for x, y in possibleMoves:
        if isOnCorner(x, y):
            return [x, y]

    # If there is no corner move to make, return a side move.
    for x, y in possibleMoves:
        if isOnSide(x, y):
            return [x, y]

    return getCornerBestMove(board, tile) # Do what the normal AI
           would do.

def printScore(board, playerTile, computerTile):
--snip--
                move = getCornerBestMove(board, playerTile)
--snip--
                move = getWorstMove(board, computerTile)
```

运行*AISim3.py*的结果与*AISim2.py*的输出类型相同，只是不同的算法将玩游戏。

#### 模拟 3 中 AI 的工作原理

`getCornerBestMove()`、`getWorstMove()`、`getRandomMove()`和`getCornerSideBestMove()`这些函数彼此相似，但使用略有不同的策略来玩游戏。其中一个使用新的`isOnSide()`函数。这类似于我们的`isOnCorner()`函数，但它在选择最高得分的移动之前检查棋盘边缘的空格。

##### 角落最佳 AI

我们已经有了一个 AI 的代码，它选择在角落移动，然后选择可能的最佳移动，因为这就是`getComputerMove()`所做的。我们只需将`getComputerMove()`的名称更改为更具描述性的名称，因此将第 162 行更改为将我们的函数重命名为`getCornerBestMove()`：

```py
def getCornerBestMove(board, computerTile):
```

由于`getComputerMove()`不再存在，我们需要将第 257 行的代码更新为`getCornerBestMove()`：

```py
                move = getCornerBestMove(board, playerTile)
```

这就是我们需要为这个 AI 做的所有工作，让我们继续。

##### 最差移动 AI

最差移动 AI 只是找到得分最低的移动并返回。它的代码很像我们在原始`getComputerMove()`算法中用来找到得分最高的移动的代码：

```py
def getWorstMove(board, tile):
    # Return the move that flips the least number of tiles.
    possibleMoves = getValidMoves(board, tile)
    random.shuffle(possibleMoves) # Randomize the order of the moves.

    # Find the lowest-scoring move possible.
    worstScore = 64
    for x, y in possibleMoves:
        boardCopy = getBoardCopy(board)
        makeMove(boardCopy, tile, x, y)
        score = getScoreOfBoard(boardCopy)[tile]
        if score < worstScore:
            worstMove = [x, y]
            worstScore = score

    return worstMove
```

`getWorstMove()`的算法从第 186 和 187 行开始与原始算法相同，但是在第 190 行开始有所不同。我们设置一个变量来保存`worstScore`，而不是`bestScore`，并将其设置为`64`，因为这是棋盘上的总位置数，也是整个棋盘填满时可能获得的最高分数。第 191 到 194 行与原始算法相同，但是第 195 行检查`score`是否小于`worstScore`，而不是检查`score`是否更高。如果`score`更小，则`worstMove`被替换为算法当前正在测试的棋盘上的移动，并且`worstScore`也会更新。然后函数返回`worstMove`。

最后，第 274 行的`getComputerMove()`需要更改为`getWorstMove()`：

```py
            move = getWorstMove(board, computerTile)
```

当这样做并运行程序时，`getCornerBestMove()`和`getWorstMove()`将相互对抗。

##### 随机移动 AI

随机移动 AI 只是找到所有有效的可能移动，然后随机选择一个。

```py
def getRandomMove(board, tile):
    possibleMoves = getValidMoves(board, tile)
    return random.choice(possibleMoves)
```

它使用`getValidMoves()`，就像所有其他 AI 一样，然后使用`choice()`来返回返回列表中的一个可能移动。

##### 检查边缘移动

在我们深入算法之前，让我们看一下我们添加的一个新的辅助函数。`isOnSide()`辅助函数类似于`isOnCorner()`函数，只是它检查移动是否在棋盘的边缘：

```py
def isOnSide(x, y):
    return x == 0 or x == WIDTH - 1 or y == 0 or y == HEIGHT - 1
```

它有一个布尔表达式，检查传递给它的坐标参数的`x`值或`y`值是否等于`0`或`7`。任何带有 0 或 7 的坐标都在棋盘的边缘。

我们将在角落-边缘最佳 AI 中使用这个函数。

##### 角落-边缘最佳 AI

角落-边缘最佳 AI 的工作方式与角落最佳 AI 非常相似，因此我们可以重用我们已经输入的一些代码。我们在`getCornerSideBestMove()`函数中定义了这个 AI：

```py
def getCornerSideBestMove(board, tile):
    # Return a corner move, a side move, or the best move.
    possibleMoves = getValidMoves(board, tile)
    random.shuffle(possibleMoves) # Randomize the order of the moves.

    # Always go for a corner if available.
    for x, y in possibleMoves:
        if isOnCorner(x, y):
            return [x, y]

    # If there is no corner move to make, return a side move.
    for x, y in possibleMoves:
        if isOnSide(x, y):
            return [x, y]

    return getCornerBestMove(board, tile) # Do what the normal AI
           would do.
```

第 210 和 211 行与我们的最佳角落 AI 中的相同，第 214 到 216 行与我们原始的`getComputerMove()` AI 中检查角落移动的算法相同。如果没有角落移动，那么第 219 到 221 行将使用`isOnSide()`辅助函数检查侧面移动。一旦所有角落和侧面移动都已检查可用性，如果仍然没有移动，那么我们将重用我们的`getCornerBestMove()`函数。由于之前没有角落移动，当代码到达`getCornerBestMove()`函数时仍然不会有任何移动，因此此函数将只查找最高得分的移动并返回。

表 16-1 回顾了我们制作的新算法。 

**表 16-1：** 用于反转棋 AI 的函数

| **函数** | **描述** |
| --- | --- |
| `getCornerBestMove()` | 如果有角落可用，则进行角落移动。如果没有角落，则找到得分最高的移动。 |
| `getCornerSideBestMove()`| 如果有角落可用，则进行角落移动。如果没有角落，则在侧面占用空间。如果没有侧面可用，则使用常规的`getCornerBestMove()`算法。 |
| `getRandomMove()` | 随机选择一个有效的移动。 |
| `getWorstMove()` | 采取导致翻转瓷砖最少的位置。 |

现在我们有了我们的算法，我们可以让它们相互对抗。

#### 比较 AI

我们编写程序，使角落最佳 AI 与最差的移动 AI 对抗。我们可以运行程序来模拟 AI 彼此对抗的表现，并使用打印的统计数据进行分析。

除了这两个 AI，我们还制作了一些其他 AI，但我们没有调用它们。这些 AI 存在于代码中，但没有被使用，因此如果我们想看看它们在比赛中的表现，我们需要编辑代码来调用它们。由于我们已经设置了一个比较，让我们看看最差的移动 AI 对抗角落最佳 AI 的表现如何。

##### 最差的移动 AI vs. 角落最佳 AI

运行程序，将`getCornerBestMove()`函数与`getWorstMove()`函数进行比较。毫不奇怪，每轮翻转最少瓷砖的策略将输掉大部分比赛：

```py
X wins: 206 (82.4%)
O wins: 41 (16.4%)
Ties:   3 (1.2%)
```

令人惊讶的是，有时最差的移动策略确实有效！`getCornerBestMove()`函数中的算法并非总是能够赢得比赛，而是大约 80％的时间。大约五分之一的时间会输！

这就是运行模拟程序的威力：您可以发现新颖的见解，如果您只是自己玩游戏，那么要意识到这一点将需要更长的时间。计算机速度更快！

##### 随机移动 AI vs. 角落最佳 AI

让我们尝试不同的策略。将第 274 行的`getWorstMove()`调用更改为`getRandomMove()`：

```py
                move = getRandomMove(board, computerTile)
```

现在运行程序，它将看起来像这样：

```py
Welcome to Reversegam!
#1: X scored 32 points. O scored 32 points.
#2: X scored 44 points. O scored 20 points.
#3: X scored 31 points. O scored 33 points.
#4: X scored 45 points. O scored 19 points.
#5: X scored 49 points. O scored 15 points.
--snip--
#249: X scored 20 points. O scored 44 points.
#250: X scored 38 points. O scored 26 points.
X wins: 195 (78.0%)
O wins: 48 (19.2%)
Ties:   7 (2.8%)
```

与最差的移动算法相比，随机移动算法`getRandomMove()`对抗角落最佳算法的表现略好一些。这是有道理的，因为做出明智的选择通常比随机选择更好，但随机选择略好于故意选择最差的移动。

##### 角落侧面最佳 AI vs. 角落最佳 AI

如果有角落空间可用，选择角落空间是一个好主意，因为角上的瓷砖永远不会被翻转。在侧面空间放置瓷砖似乎也是一个不错的主意，因为它被包围和翻转的方式较少。但是，这种好处是否超过了放弃会翻转更多瓷砖的移动？让我们通过将角落最佳算法与角落侧面最佳算法进行比较来找出答案。

将第 274 行的算法更改为使用`getCornerSideBestMove()`：

```py
                move = getCornerSideBestMove(board, computerTile)
```

然后再次运行程序：

```py
Welcome to Reversegam!
#1: X scored 27 points. O scored 37 points.
#2: X scored 39 points. O scored 25 points.
#3: X scored 41 points. O scored 23 points.
--snip--
#249: X scored 48 points. O scored 16 points.
#250: X scored 38 points. O scored 26 points.
X wins: 152 (60.8%)
O wins: 89 (35.6%)
Ties:   9 (3.6%)
```

哇！这是意想不到的。选择侧面空间而不是翻转更多瓷砖的空间似乎是一个糟糕的策略。侧面空间的好处不足以抵消翻转对手更少瓷砖的成本。我们能确定这些结果吗？让我们再次运行程序，但这次通过在*AISim3.py*中将第 278 行更改为`NUM_GAMES = 1000`来玩 1,000 场比赛。现在，程序可能需要几分钟才能在您的计算机上运行，但如果您手动操作，可能需要*几周*的时间！

您将看到，1,000 场比赛的更准确的统计数据与 250 场比赛的统计数据几乎相同。似乎选择翻转最多瓷砖的移动比选择侧面移动更好。

我们刚刚使用编程找出了哪种游戏策略最有效。当您听说科学家使用计算机模型时，他们正在做的就是这个。他们使用模拟重新创建一些真实世界的过程，然后在模拟中进行测试，以了解更多关于真实世界的信息。

### 摘要

本章没有涵盖新游戏，而是对反转棋进行了各种策略建模。如果我们认为在反转棋中采取侧面移动是一个好主意，我们将不得不花费几周，甚至几个月的时间仔细玩反转棋游戏，并写下结果来测试这个想法。但是，如果我们知道如何编写计算机来玩反转棋，那么我们可以让它为我们尝试不同的策略。如果您仔细想想，计算机在几秒钟内执行了数百万行我们的 Python 程序！您对反转棋模拟的实验可以帮助您更多地了解如何在现实生活中玩它。

事实上，这一章将成为一个很好的科学展览项目。您可以研究哪种移动方式导致对其他移动方式的最多胜利，并且您可以对哪种是最佳策略提出假设。运行几次模拟后，您可以确定哪种策略最有效。通过编程，您可以将任何棋盘游戏的模拟制作成一个科学展览项目！这一切都是因为您知道如何逐步指导计算机做这些事情，一行一行地。您可以用计算机的语言并让它为您进行大量的数据处理和数值计算。

这本书中的基于文本的游戏就到此为止了。尽管它们很简单，但只使用文本的游戏也可以很有趣。但是，大多数现代游戏使用图形、声音和动画使它们更加令人兴奋。在本书的其余章节中，您将学习如何使用名为`pygame`的 Python 模块创建具有图形的游戏。


