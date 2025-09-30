# LAMBDA APP打包步骤

1. 安装pyinstaller

   `pip install pyinstaller`

2. 生成lambda_app.spec:

    `pyi-makespec --collect-data=gradio_client --collect-data=gradio lambda_app.py`

   生成的文件如下，需要手动在Analysis中加入module_collection_mode={ 'gradio': 'py',},

   ```
   # -*- mode: python ; coding: utf-8 -*-
   from PyInstaller.utils.hooks import collect_data_files
   
   datas = []
   datas += collect_data_files('gradio_client')
   datas += collect_data_files('gradio')
   
   
   a = Analysis(
       ['lambda_app.py'],
       pathex=[],
       binaries=[],
       datas=datas,
       hiddenimports=[],
       hookspath=[],
       hooksconfig={},
       runtime_hooks=[],
       excludes=[],
       noarchive=False,
       optimize=0,
       module_collection_mode={ 'gradio': 'py',},
   )
   pyz = PYZ(a.pure)
   
   exe = EXE(
       pyz,
       a.scripts,
       [],
       exclude_binaries=True,
       name='lambda_app',
       debug=False,
       bootloader_ignore_signals=False,
       strip=False,
       upx=True,
       console=True,
       disable_windowed_traceback=False,
       argv_emulation=False,
       target_arch=None,
       codesign_identity=None,
       entitlements_file=None,
   )
   coll = COLLECT(
       exe,
       a.binaries,
       a.datas,
       strip=False,
       upx=True,
       upx_exclude=[],
       name='lambda_app',
   )
   ```

3. 打包

   `pyinstaller lambda_app.spec`

   最终：399266 INFO: Build complete! The results are available in: /Users/stephensun/Desktop/LAMBDA_code/LAMBDA/dist

