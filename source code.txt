import time
data = {}
code = open(input("code file:"),"r")
runable = code.read()

on = 0

while on < len(runable)-1:
    if runable[on] == '@':
        on += 1
        name = ""
        value = ""
        while runable[on] != "_":
            name += runable[on]
            on += 1
        on += 1
        if runable[on] == "[":
            on += 1
            while runable[on] != "]":
                value += runable[on]
                on += 1
            data.update({name:value})
        else:
            while runable[on] != ".":
                if runable[on] == "$":
                    on += 1
                    varRef = ""
                    while runable[on] != "<":
                        varRef += runable[on]
                        on += 1
                    value += str(data[varRef])
                value += runable[on]
                on += 1
                value = value.replace('<','')
                data.update({name:int(value)})


    if runable[on] == '#':
        on += 1
        value = ""
        while runable[on] != ".":
            if runable[on] == "$":
                on += 1
                varRef = ""
                while runable[on] != "<":
                    varRef += runable[on]
                    on += 1
                value += str(data[varRef])
            value += runable[on]
            on += 1
            value = value.replace('<','')
        print(value)

    if runable[on] == '+':
        on += 1
        var1 = ""
        var2 = ""
        var3 = ""
        while runable[on] != "_":
            var3 += runable[on]
            on += 1
        on += 1
        while runable[on] != "_":
            var1 += runable[on]
            on += 1
        on += 1
        while runable[on] != ".":
            var2 += runable[on]
            on += 1
        data[var3] = data[var1] + data[var2]

    if runable[on] == '-':
        on += 1
        var1 = ""
        var2 = ""
        var3 = ""
        while runable[on] != "_":
            var3 += runable[on]
            on += 1
        on += 1
        while runable[on] != "_":
            var1 += runable[on]
            on += 1
        on += 1
        while runable[on] != ".":
            var2 += runable[on]
            on += 1
        data[var3] = data[var1] - data[var2]

    if runable[on] == '*':
        on += 1
        var1 = ""
        var2 = ""
        var3 = ""
        while runable[on] != "_":
            var3 += runable[on]
            on += 1
        on += 1
        while runable[on] != "_":
            var1 += runable[on]
            on += 1
        on += 1
        while runable[on] != ".":
            var2 += runable[on]
            on += 1
        data[var3] = data[var1] * data[var2]

    if runable[on] == '/':
        on += 1
        var1 = ""
        var2 = ""
        var3 = ""
        while runable[on] != "_":
            var3 += runable[on]
            on += 1
        on += 1
        while runable[on] != "_":
            var1 += runable[on]
            on += 1
        on += 1
        while runable[on] != ".":
            var2 += runable[on]
            on += 1
        data[var3] = data[var1] / data[var2]

    if runable[on] == '=':
        on += 1
        var1 = ""
        var2 = ""
        var3 = ""
        while runable[on] != "_":
            var3 += runable[on]
            on += 1
        on += 1
        while runable[on] != "_":
            var1 += runable[on]
            on += 1
        on += 1
        while runable[on] != ".":
            var2 += runable[on]
            on += 1
        if data[var1] == data[var2]:
            data[var3] = 1
        else:
            data[var3] = 0

    if runable[on] == '<':
        on += 1
        var1 = ""
        var2 = ""
        var3 = ""
        while runable[on] != "_":
            var3 += runable[on]
            on += 1
        on += 1
        while runable[on] != "_":
            var1 += runable[on]
            on += 1
        on += 1
        while runable[on] != ".":
            var2 += runable[on]
            on += 1
        if data[var1] < data[var2]:
            data[var3] = 1
        else:
            data[var3] = 0

    if runable[on] == ">":
        on += 1
        varRef = ""
        while runable[on] != ".":
            varRef += runable[on]
            on += 1
        data[varRef] = int(input(">"))
    
    if runable[on] == "?":
        on += 1
        varRef=""
        while runable[on] != "[":
            varRef += runable[on]
            on += 1
        on += 1
        if data[varRef] == 1:
            void = 0
        if data[varRef] == 0:
            brackets = 1
            while runable[on] != "]" and brackets > 0:
                on += 1
                if(runable[on] == "["):
                    brackets += 1
                if(runable[on] == "]"):
                    brackets -= 1
            on += 1

    if runable[on] == "$":
        on += 1
        varRef = ""
        while runable[on] != ".":
            varRef += runable[on]
            on += 1
        run(data[varRef])

    if runable[on] == ",":
        to = on

    if runable[on] == "'":
        on = to
        on += 1
    on += 1

time.sleep(100)

