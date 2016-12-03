```
@http.route('/user/avatar', tyep="http", auth="user", mehtod=['POST'], csrf=False)
    def update_avatar(self, *args, **kwargs):
        """更新用户头像"""
        user = request.env.user
        resp_msg = {}
        avatar_value = kwargs.get('avatar_file', '')   # 上传文件起名为 avatar_file
        if avatar_value:
            avatar_b64 = base64.b64encode(avatar_value.read())
            try:
                user.image = tools.image_resize_image(avatar_b64)
                resp_msg['message'] = 'upload success'
            except IOError as e:
                resp_msg['message'] = 'cannot identify image file'
        else:
            resp_msg['message'] = 'please name the avatar file avatar_file'
        resp_json = json.dumps({'result': resp_msg})
        response = request.make_response(resp_json)
        return response

```
