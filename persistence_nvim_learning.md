# **plugin-persistence.nvim**
处理窗口在cwd退出后的状态保持

使用 `require("persistence").load({last = true})` 即可以恢复上次退出 vim的状态，可以将此键作为一个映射 调出 也可以设置在init.vim中，当vim没有参数（即不加目录或者文件时使用时）加载上次退出vim时候的布局
- autoload ,set this on init.lua  
    ```
    local args = vim.api.nvim_get_vvar("argv")  
    if #args >2 then
    else 
        require("persistence").load({ last = true})
    end
    -- :h nvim_get_vvar / h:  v:argv 
    ```
当使用vim不带参数的启动的时候恢复到上一次退出vim的状态（打开的buffer,windows的布置）
- 使用keymap, 选择时机去启动 上次退出时候的界面

    ```lua
    --recommanded config
    -- restore the session for the current directory
    vim.api.nvim_set_keymap("n", "<leader>qs", [[<cmd>lua require("persistence").load()<cr>]], {})

    -- restore the last session
    vim.api.nvim_set_keymap("n", "<leader>ql", [[<cmd>lua require("persistence").load({ last = true })<cr>]], {})

    -- stop Persistence => session won't be saved on exit
    vim.api.nvim_set_keymap("n", "<leader>qd", [[<cmd>lua require("persistence").stop()<cr>]], {})
    ```
