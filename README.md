# go-captcha
Package captcha implements generation and click location verification of image CAPTCHAs. 


[![License](https://img.shields.io/github/license/wenlng/go-captcha.svg)](https://github.com/wenlng/go-captcha/blob/master/LICENSE)
[![Version](https://img.shields.io/github/tag/wenlng/go-captcha.svg)](https://github.com/wenlng/go-captcha/releases)
[![Go Report Card](https://goreportcard.com/badge/github.com/wenlng/go-captcha)](https://goreportcard.com/report/github.com/wenlng/go-captcha)
[![GoDoc](https://godoc.org/github.com/wenlng/go-captcha?status.svg)](https://godoc.org/github.com/wenlng/go-captcha)

- Github：[https://github.com/wenlng/go-captcha](https://github.com/wenlng/go-captcha)
- Example Code：[https://github.com/wenlng/go-captcha-example](https://github.com/wenlng/go-captcha-example)
- Demo：[http://47.104.180.148:8081/go_captcha_demo](http://47.104.180.148:8081/go_captcha_demo)
- Author Website: [http://witkeycode.com](http://witkeycode.com)

<div align="center">
    <img src="http://47.104.180.148/go-captcha/go-captcha-01.png?v=1" alt="Reward Support">
    <br/>
    <br/>
    <img src="http://47.104.180.148/go-captcha/go-captcha-02.png?v=1" alt="Reward Support">
    <br/>
    <br/>
    <img src="http://47.104.180.148/go-captcha/go-captcha.jpg?v=1" alt="Reward Support">
    <br/>
    <br/>   
</div>
<br>

- Installation of proxy go module in China
>
>GoProxy https://github.com/goproxy/goproxy.cn
>
>AliProxy： https://mirrors.aliyun.com/goproxy/
>
>OfficialProxy： https://goproxy.io/
>
>ChinaProxy：https://goproxy.cn
>
>Other：https://gocenter.io

### Set Proxy of Go module 
- Window
```shell script
set GO111MODULE=on
set GOPROXY=https://goproxy.io,direct

### The Golang 1.13+ can be executed directly
go env -w GO111MODULE=on
go env -w GOPROXY=https://goproxy.io,direct
```
- Linux or Mac
```shell script
vi vim ~/.bash_profile
export GO111MODULE=on
export GOPROXY=https://goproxy.io,direct
source ~/.bash_profile
```

### Install Module
```
go get -u github.com/wenlng/go-captcha
```

### Import Module
```go
package main

import "github.com/wenlng/go-captcha/captcha"

func main(){
   // ....
}
```

### Quick use
```go
package main
import (
    "fmt"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
    // Captcha Single Instances
    capt := captcha.GetCaptcha()
    
    // ==========================
    // Config that must be set
    // --------------------------
    // Set font absolute path
    capt.SetFont([]string{
        "/__example/resources/fonts/fzshengsksjw_cu.ttf",
        "/__example/resources/fonts/fzssksxl.ttf",
    })
    
    // Set background image absolute path
    capt.SetBackground([]string{
        "/__example/resources/images/1.jpg",
        "/__example/resources/images/2.jpg",
    })
    
    // Generate Captcha
    dots, b64, tb64, key, err := capt.Generate()
    if err != nil {
        panic(err)
        return
    }
    
    // Main image base64 code
    fmt.Println(len(b64))
    
    // Thumb image base64 code
    fmt.Println(len(tb64))
    
    // Only key
    fmt.Println(key)
    
    // Dot data For verification
    fmt.Println(dots)
}

```

### Method Instructions
- New Instances or Get Single Instances
```go
package main
import (
    "fmt"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
	// Captcha Instances
    // capt := captcha.NewCaptcha() 
    
    // Captcha Single Instances
    capt := captcha.GetCaptcha()

    // ====================================================
    fmt.Println(capt)

}
```

- Set Chars
```go
package main
import (
    "fmt"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
    capt := captcha.GetCaptcha()
    
    // ====================================================
    // Method: SetRangChars (chars []string) error;
    // Desc: Set random char of captcha
    // ====================================================
    // Letter
    //chars := "abcdefghijklmnopqrstuvwxyz0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"
    //_ = capt.SetRangChars(strings.Split(chars, ""))
    
    // Two Letter
    //chars := []string{"HE","CA","WO","NE","HT","IE","PG","GI","CH","CO","DA"}
    //_ = capt.SetRangChars(chars)

    // Chinese Char
    chars := []string{"你","好","呀","这","是","点","击","验","证","码","哟"}
    _ = capt.SetRangChars(chars)

    // ====================================================
    fmt.Println(capt)
}
```

### Set configuration
```go
package main
import (
    "fmt"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
    capt := captcha.GetCaptcha()
    
    // ====================================================
    // Method: SetBackground(color []string);
    // Desc: Set random image of captcha background
    // ====================================================
    capt.SetBackground([]string{
        "/__example/resources/images/1.jpg",
        "/__example/resources/images/2.jpg",
    })

    // ====================================================
    // Method: SetFont(fonts []string);
    // Desc: Set random font of captcha text
    // ====================================================
    capt.SetFont([]string{
        "/__example/resources/fonts/fzshengsksjw_cu.ttf",
        "/__example/resources/fonts/fzssksxl.ttf",
    })

    // ====================================================
    // Method: SetImageSize(size *Size);
    // Desc: Set size of captcha
    // ====================================================
    capt.SetImageSize(&captcha.Size{300, 300})

    // ====================================================
    // Method: SetThumbSize(size *Size);
    // Desc: Set size of captcha thumb
    // ====================================================
    capt.SetThumbSize(&captcha.Size{150, 40})

    // ====================================================
    // Method: SetFontDPI(val int);
    // Desc: Set random DPI of captcha font, The best is 72
    // ====================================================
    capt.SetFontDPI(72)

    // ====================================================
    // Method: SetTextRangLen(val *captcha.RangeVal);
    // Desc: Set random length of captcha text
    // ====================================================
    capt.SetTextRangLen(&captcha.RangeVal{6, 7})

    // ====================================================
    // Method: SetRangFontSize(val *captcha.RangeVal);
    // Desc: Set random size of captcha text
    // ====================================================
    capt.SetRangFontSize(&captcha.RangeVal{32, 42})

    // ====================================================
    // Method: SetRangCheckTextLen(val *captcha.RangeVal);
    // Desc:Set random length of check text
    // ====================================================
    capt.SetRangCheckTextLen(&captcha.RangeVal{2, 4})

    // ====================================================
    // Method: SetRangCheckFontSize(val *captcha.RangeVal);
    // Desc:Set random size of check text
    // ====================================================
    capt.SetRangCheckFontSize(&captcha.RangeVal{24, 30})
    
    // ====================================================
    // Method: SetTextRangFontColors(colors []string);
    // Desc: Set random hex color of captcha text
    // ====================================================
    capt.SetTextRangFontColors([]string{
        "#1d3f84",
        "#3a6a1e",
    })

    // ====================================================
    // Method: SetImageFontAlpha(val float64);
    // Desc:Set alpha of captcha font
    // ====================================================
    capt.SetImageFontAlpha(0.5)

    // ====================================================
    // Method: SetTextRangAnglePos(pos []*RangeVal);
    // Desc:Set angle of captcha text
    // ====================================================
    capt.SetTextRangAnglePos([]*captcha.RangeVal{
        {1, 15},
        {15, 30},
        {30, 45},
        {315, 330},
        {330, 345},
        {345, 359},
    })

    // ====================================================
    // Method: SetImageFontDistort(val int);
    // Desc:Set distort of captcha font
    // ====================================================
    capt.SetImageFontDistort(captcha.ThumbBackgroundDistortLevel2)
  
    // ====================================================
    // Method: SetThumbBgColors(colors []string);
    // Desc: Sets the random hex color of the captcha thumb background
    // ====================================================
    capt.SetThumbBgColors([]string{
        "#1d3f84",
        "#3a6a1e",
    })

    // ====================================================
    // Method: SetThumbBackground(colors []string);
    // Desc:Set random image of captcha thumb background
    // ====================================================
    capt.SetThumbBackground([]string{
        "/__example/resources/images/r1.jpg",
        "/__example/resources/images/r2.jpg",
    })

    // ====================================================
    // Method: SetThumbBgDistort(val int);
    // Desc:Set distort of captcha thumb
    // ====================================================
    capt.SetThumbBgDistort(captcha.ThumbBackgroundDistortLevel2)

    // ====================================================
    // Method: SetThumbBgCirclesNum(val int);
    // Desc:Set circles number of captcha background
    // ====================================================
    capt.SetThumbBgCirclesNum(20)

    // ====================================================
    // Method: SetThumbBgSlimLineNum(val int);
    // Desc:Set line number of captcha background
    // ====================================================
    capt.SetThumbBgSlimLineNum(3)
    

    // ====================================================
    fmt.Println(capt)
}
```

### Generate Captcha Data
```go
package main
import (
    "fmt"
    "github.com/wenlng/go-captcha/captcha"
)

func main(){
    capt := captcha.GetCaptcha()
    
    // set configuration ...
    // ==========================
    capt.SetFont([]string{
        "/__example/resources/fonts/fzshengsksjw_cu.ttf",
        "/__example/resources/fonts/fzssksxl.ttf",
    })
    capt.SetBackground([]string{
        "/__example/resources/images/1.jpg",
        "/__example/resources/images/2.jpg",
    })
    
    // generate ...
    // ====================================================
    // dots:  Character position information
    //  - {"0":{"Index":0,"Dx":198,"Dy":77,"Size":41,"Width":54,"Height":41,"Text":"SH","Angle":6,"Color":"#885500"} ...}
    // imageBase64:  Verify the clicked image
    // thumbImageBase64: Thumb displayed
    // key: Only Key
    // ====================================================
    dots, imageBase64, thumbImageBase64, key, err := capt.Generate()
    if err != nil {
        panic(err)
        return
    }
    fmt.Println(len(imageBase64))
    fmt.Println(len(thumbImageBase64))
    fmt.Println(key)
    fmt.Println(dots)
}
```

### Fronted Example Api Params
```
// Example: Get captcha data
API = http://....../captcha/captcha-data
    Respose Data = {
        "code": 0,
        "image_base64": "...",
        "thumb_base64": "...",
        "captcha_key": "...",
    }     

// Example: Post check data
API = http://....../captcha/check-data
    Request Data = {
        dots: "x1,y1,x2,y2,...."
        key: "......"
    }
```


<div align="center">
    <img src="http://47.104.180.148/reward-support.png?v=1" alt="Reward Support">
</div>
<br/>

## LICENSE
    MIT
