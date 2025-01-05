
- Step 1 : Create the Hugo Site 
    hugo new site --force . ✅
- Step 2 : Install blowfish theme
    I use Quick start using Hugo
    
    hugo mod init github.com/agentifyanchor/blog ✅
    hugo mod tidy ✅

    Create config/_default/module.toml
    add this code 
    
    [[imports]]
    path = "github.com/nunocoracao/blowfish/v2"

    run 
    hugo server ✅ 
    site work fine in http://localhost:1313/

- Step 4 : Integrate with Front matter    
Instable with beta version 😖