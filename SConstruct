import os

env = DefaultEnvironment()

AddOption('--doc-format',  dest='doc_format', action="store", default='html',
          metavar='FORMAT', help='Documentation format (markdown or html)')
AddOption('--verbose', dest='verbose', action='store_true', default=False,
          help='Be verbose')

InkscapeBuilder = Builder(action = Action('inkscape -z -e $TARGET $SOURCE'),
                          suffix = '.png',
                          src_suffix = '.svg')
env.Append(BUILDERS = {'InkscapeBuilder': InkscapeBuilder})

def ConvertSVGs(env, imgdir, width):
    img = env.Clone()
    img['PNGWIDTH'] = width
    
    for image in imgdir.glob('*.svg'):
        tgt = os.path.join('build', image.path.replace('.svg', '.png'))
        img.InkscapeBuilder(tgt, image)

ConvertSVGs(env, Dir('images'), 800)
ConvertSVGs(env, Dir('images').Dir('icons'), 24)

env.VariantDir('build/', 'book/')
SConscript('build/SConscript', 'env')